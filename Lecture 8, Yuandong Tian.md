# Lecture 8

This [lecture](https://www.youtube.com/live/wm9-7VBpdEo?si=6hkWWZW0M4GxwtDB) exposes the **inadequacies of LLMs** in complex, large-scale planning tasks. While scaling alone helps marginally, more robust strategies merge **symbolic solvers** with **neural** approaches—LLMs parse user intent or generate partial solutions, and symbolic algorithms ensure **feasibility** or **optimality**. Further, “search-augmented” models can learn from solver traces and iteratively refine their internal plans, yielding shorter paths and higher success rates. Lastly, experiments on modular arithmetic suggest that neural networks may **spontaneously adopt symbolic representations**, hinting that future large models could unify neural and symbolic paradigms.


---

## Introduction

| **Topic**                | **Notes**                                                                                                                                                                                                                                    |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Key Challenge**                              | Despite LLMs’ success in **natural language** tasks, they **struggle** with complex, multi-step planning (e.g., scheduling, travel itineraries, meeting constraints).                                                                                                                            |
| **Goals & Outline**                            | - Explore methods to **overcome LLM planning weaknesses**. <br>- Present **three solution pathways**: (1) Scaling law (bigger LLMs), (2) **Hybrid symbolic + neural** systems, (3) Investigating **emergent symbolic representations** in neural nets.                                                                                 |

---

## Travel Planning Example & LLM Shortcomings

| **Topic**               | **Notes**                                                                                                                                                                                                                                   |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Travel-Planning Experiment**               | - **Task**: Given user constraints (destinations, budget, travel dates), produce a **feasible, optimal** itinerary. <br>- Even strong models (e.g., GPT-4 Turbo) yield low success (pass rate **0.6%**). <br>- Fine-tuning or providing ground-truth data helps minimally (4.4% pass rate).                                           |
| **Performance Over Time**                    | - Many believe “model improvements every few weeks” fix all. However, new tests (e.g., **OpenAI O(1)**) show that **scalability** alone does not resolve large-scale planning. <br>- As planning complexity (variables, constraints) grows, success rates tend toward **0%** even for the latest models.                                      |
| **Core Weakness**                            | - LLMs handle language well but falter in **complex combinatorial tasks** (e.g., multi-city itineraries, multi-variable constraints). <br>- Larger models improve on *smaller tasks*, but fail dramatically on scaled-up versions.                                                            |

---

## Three Possible Solutions

| **Topic** | **Notes**                                                                                                                                                                                                                                                                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Solution 1: Scaling**         | - Keep increasing **model size**, data, and compute. <br>- Very expensive and no *guarantee* it fully solves combinatorial or large-scale constraints.                                                                                                                                                                                                                                      |
| **Solution 2: Hybrid Systems**  | - Pair **symbolic solvers** (guaranteed search or optimization) with **deep LLMs** (great at natural language). <br>- Symbolic solvers do not “speak language,” but excel at *optimal solutions*. LLMs handle user requests, parse them, etc.                                                                                                                                               |
| **Solution 3: Emergent Symbolic** | - Investigate if neural networks themselves develop **symbolic-like** internal structures. <br>- Potential for purely neural solutions that *act* symbolic.                                                                                                                                                                                                                                     |

---

## Hybrid Systems (Solution 2)

### Tool Use: LLM + Symbolic Solver

| **Topic**                   | **Notes**                                                                                                                                                                                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Travel Plan + MILP**                           | 1. **LLM** translates user input → **JSON**. <br>2. **Mixed Integer Linear Programming (MILP)** solver finds optimal plan (feasible itinerary). <br>3. **JSON** solution → LLM → final user-friendly text. <br>- Demo is **real-time** (~2.5s for translation + <1s for solver). Accepted at EMNLP 2023.                              |
| **Multi-Round Dialogue**                         | - Real planning often requires back-and-forth Q&A: user clarifications, budget vs. experience, etc. <br>- Fine-tuned an agent with “**APEC constitution**” (Accuracy, Proactivity, Efficiency, Credibility) to gather all needed info **minimally** then pass it to solver.                                                                      |
| **Agent Constitution & DPO**                     | - Approach to align agent behaviors (asking relevant questions, not hallucinating, etc.). <br>- **Direct Preference Optimization (DPO)** can iteratively tune agent performance along multiple axes (accuracy, adaptiveness).                                                                             |
| **Agents as Judges**                             | - Another idea: let a *second agent* check each **step** of the first agent’s plan to provide **richer feedback** (beyond just final outcome). <br>- Improves agent’s planning by pinpointing errors earlier.                                                                                               |

### Using Solver Traces for Training (SearchFormer, DualFormer)

| **Topic**                 | **Notes**                                                                                                                                                                                                                                                       |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **SearchFormer**                                | - Strategy: capture **A* search traces** (or other solver expansions) as training data. <br>- Model first predicts the **search trace**, then from that trace predicts the final solution. <br>- Greatly **reduces data/parameter requirements** vs. direct “solution-only” training.                            |
| **Maze & Sokoban**                              | - Maze: 3×3, 30×30 tasks → *Search-augmented training* yields higher accuracy with fewer samples. <br>- Sokoban: Pushing boxes requires careful planning; again, solver expansions help.                                                                                                                         |
| **Beyond A***                                   | - Once we have a search-augmented model, we can sample multiple traces → pick best/shortest → retrain. <br>- Over iterations, the model finds **shorter** solution paths *and* higher optimality.                                                                                                               |
| **DualFormer**                                  | - **V2**: randomly *drop parts* of search trace → trains the model to handle both “system 1” (quick direct plan) and “system 2” (long reasoning). <br>- The model **auto-selects** fast or slow approach. <br>- Works for math tasks (AugMATH) with shorter chain-of-thought but improved accuracy.                                               |

### End-to-End Training with Solvers

| **Topic**       | **Notes**                                                                                                                                                                                                                                                      |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Non-Linear Optimization**          | - Many real tasks: objective is non-linear, constraints are combinatorial. (Device placement, photonic design, etc.) <br>- LLM or neural approach alone is insufficient, but standard solver alone can’t parse all user scenarios.                                                                              |
| **Embedding Table Sharding**         | - Example: Minimizing latency while respecting GPU memory constraints. <br>- Combine a **learned surrogate cost** + linear solver → solution is backpropagated. <br>- Gains speed & solution quality vs. purely heuristic or RL-based approaches.                                                                |
| **Photonic Design**                  | - 80×80 grid, wave interference for routing light. <br>- Non-linear optical simulation + linear manufacturing constraints. <br>- End-to-end approach gives stable convergence compared to naive “pass-through” or purely black-box search, which is slow/unstable.                                                   |
| **Limitations**                      | - If objective is non-differentiable, or if we must call the solver at every iteration, it’s expensive. <br>- Ongoing research in partial relaxations, approximate gradients, and better ways to reduce solver overhead.                                                                                     |

---

## Emergent Symbolic Structures (Solution 3)

| **Topic**                          | **Notes**                                                                                                                                                                                                                                                                                     |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **LLM Debate**                                          | 1. **Scaling** unlocks emergent capabilities → eventually everything. <br>2. LLMs are mostly **memorizing** or doing pattern matching with no true symbolic reasoning. <br>- Example: Apple’s “GSM8K…Symbolic?” paper shows model performance drastically drops if random text is inserted, implying possible shallow “tricks.”                   |
| **Modular Addition Example**                             | - Even a simple neural net trained on “(A + B) mod D” can develop **Fourier-like** internal encodings. <br>- Surprising that the net solution strongly **matches** symbolic expansions (e.g., factorizing solutions reveals a ring structure).                                                                                                  |
| **Algebraic Explanation**                                | - For a 2-layer net with quadratic activation, the solution space forms a **semi-ring** under certain definitions. <br>- Summation-based constraints can combine partial solutions → produce global solutions exactly matching the network’s gradient descent results.                                                                        |
| **Implications**                                        | 1. Neural nets can spontaneously learn **symbolic** or algebraic structures. <br>2. Perhaps we can skip gradient descent by constructing solutions algebraically. <br>3. Larger LLMs might contain hidden symbolic patterns for advanced reasoning, though further research is needed to “open the black box.”                                        |

---