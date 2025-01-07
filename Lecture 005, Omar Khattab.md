# Lecture 5

This [lecture](https://www.youtube.com/live/JEMYuzrKLUw?si=pjz6Rw34FloJmT_M) explains how **compound AI systems**—modular architectures of multiple LM-based steps—offer greater **accuracy**, **control**, and **debuggability** than a single monolithic LM. Using the **DSPy** approach, developers write **normal Python code** to define modular “signatures” for tasks like query generation or answer synthesis. **Optimizers** then tune the system’s **instructions** and **few-shot examples**, using techniques like **bootstrapping** and **Bayesian optimization** to achieve significantly improved performance. This modular paradigm allows rapid iteration, easier debugging, and reuse of components across tasks, suggesting a clear path toward building more reliable and maintainable AI systems.

---

## Introduction

| **Topic**               | **Notes**                                                                                                                                                                                                                                        |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Lecture Focus**                             | - Discusses building **compound AI systems**—modular architectures where **language models** (LMs) serve as parts of a larger program (not just a single black-box). <br>- Introduces **DSPy** (“declaratively self-improving Python”) as a framework for modular programming with LMs. |
| **Motivation**                                | - **Monolithic LMs** (like ChatGPT) are impressive but error-prone and hard to control/debug. <br>- Modular design and explicit control flow can help isolate errors, improve transparency, and simplify iteration.                                          |
| **Key Example**                               | - **ChatGPT** can provide code suggestions but can produce subtle bugs (e.g., data races when parallelizing code). <br>- Real-world AI tasks need reliability and “explainability” that purely monolithic LMs often struggle to deliver.                                                        |

---

## Compound AI Systems vs. Single LMs

| **Topic**               | **Notes**                                                                                                                                                                                                                                  |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Definition: Compound AI System**           | - A system composed of **multiple LM modules** (or steps) each handling specialized tasks (e.g., retrieving data, generating partial solutions, verifying facts). <br>- Contrasts with a single end-to-end LM that tries to do everything in one pass.                                |
| **Advantages of Modular Approach**           | 1. **Transparency & Debugging**: We can inspect intermediate steps and see where errors occur. <br>2. **Efficiency**: Offload knowledge retrieval to external sources (e.g., search engines) instead of forcing the LM to hold all knowledge. <br>3. **Inference Time Gains**: Complex tasks can be broken into structured steps. |
| **Examples**                                 | - **Retrieval-Augmented Generation (RAG)**: LM retrieves relevant documents first, then composes answers. <br>- **Multi-Hop QA**: LM iteratively queries a knowledge base or search to find partial facts, combining them for a final answer. <br>- **AlphaCode-Style**: Decompose coding tasks, generate multiple solutions, run tests, pick the best. |
| **Challenges**                                | - LMs are “**stringly typed**” and sensitive to exact prompts. <br>- Combining multiple modules often requires thousands of tokens of instructions, leading to brittle solutions. <br>- Hard to systematically share or reuse “prompt engineering” across different tasks/models.                                           |

---

## Programming Paradigm & DSPy Framework

| **Topic**          | **Notes**                                                                                                                                                                                                  |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Goal: Natural Language “Functions”**   | - **DSPy** aims to let developers write standard **Python code** that describes modules in high-level “signatures” or specifications (e.g., `def retrieve(query) -> list of docs`). <br>- LMs then fill in fuzzy, learned behaviors for each function.                             |
| **Key Concepts**                         | 1. **Module Signature:** Each LM-powered function has input/output specifications in natural language form. <br>2. **Program Logic:** The developer writes loops, conditionals, etc. to orchestrate how modules connect. <br>3. **No Hardcoding Prompts:** DSPy automatically compiles or optimizes short signatures into workable prompts. |
| **Advantages**                            | - **Portability & Modularity:** By abstracting “how the LM does something” away from “what the module is supposed to do,” developers can swap in new LMs or tweak steps without rewriting massive prompts. <br>- **Programmable Flow:** Real Python structures handle branching, loops, retries, etc.               |

---

## Optimizing LMs via DSPy

| **Topic**      | **Notes**                                                                                                                                                                                                                              |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Need for Optimization**            | - Even with modular code, LMs must be **prompted or fine-tuned** effectively to get high accuracy. <br>- “Out-of-the-box” prompts often yield mediocre results, especially with multi-step or specialized tasks.                                                                      |
| **Two Key Levers**                   | 1. **Instructions**: Written guidance or “task description” telling an LM how to behave. <br>2. **Demonstrations (Few-Shot Examples)**: Sample inputs/outputs demonstrating correct responses or transformations.                                                                      |
| **DSPy’s “Optimizer” Concept**       | - Treats prompts and instructions as **parameters**. <br>- Given training data or examples plus a user-defined **evaluation metric**, DSPy searches for better prompt configurations that maximize performance. <br>- No direct gradient access required; works with high-level LM APIs.                       |
| **Metrics**                           | - The user must define a **metric** (like accuracy, or “is the final answer factually correct?”). <br>- The optimizer tries various prompt combos (instructions + examples) and picks the combination that yields highest metric performance on validation data.                                 |

---

## Techniques for Prompt Optimization

| **Topic**          | **Notes**                                                                                                                                                                                                                                               |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Bootstrapping (Self-Generated Demos)**| 1. Run a “basic/dumb” version of the program on training inputs. <br>2. Collect successful input-output pairs for each module. <br>3. Use these pairs as few-shot examples in future prompts. <br>4. Iteratively refine or expand the example pool as performance improves.                             |
| **Instruction Optimization**             | - Use the LM itself to propose or refine instructions. <br>- Provide context about the entire pipeline (e.g., “this is a multi-hop QA system”) and summary of mistakes or successes. <br>- The LM can suggest better instructions (“Be sure to always cite sources accurately”).                                 |
| **Coordinate vs. Joint Updates**         | - **Coordinate Ascent**: Fix all modules but one, optimize that module’s prompt, repeat for the next, etc. <br>- **Joint Updates**: Ask the LM to propose new instructions/demos for **all modules** at once. More flexible, but can be more expensive or model-confusing.                                |
| **Surrogate / Bayesian Optimization**    | - Approaches like **MEO** (Modular Prompt & Example Optimization) build a model that predicts performance of prompt combos. <br>- Use it to sample the most promising prompt configurations, test them, and iteratively refine.                                                                            |

---

## Empirical Results & Use Cases

| **Topic**             | **Notes**                                                                                                                                                                                                                      |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Performance Benchmarks**                 | - On tasks like **Multi-Hop QA**, combining modules for retrieval + generation can outperform a single large LM prompting. <br>- Even older models (e.g., T5) can compete with bigger modern LMs if carefully fine-tuned or prompted in a compound pipeline.                 |
| **LangProbe Benchmark**                     | - A set of tasks (QA, classification, inference) with varying module counts. <br>- Shows that **few-shot demos** + instructions consistently improve accuracy (often by 10+ points). <br>- MEO outperforms simpler random or coordinate-based prompt tuning in many tasks. |
| **Real-World Adoption**                     | - **University of Toronto** used DSPy to dominate a medical QA competition by 20 points over the 2nd place. <br>- **University of Maryland** applied it to a suicide detection classifier, beating expert-engineered prompts by 40–50%.                                      |
| **Open-Source & Industry**                  | - Organizations like JetBlue, Walmart, VMware, Sephora, and more use or experiment with DSPy. <br>- Demonstrates that “**compound AI** + **automated prompt optimization**” is practical at scale.                                                                             |

---

## Broader Lessons & Future Directions

| **Topic**     | **Notes**                                                                                                                                                                                              |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Modularity in AI**                | - Similar to how **layers in neural nets** improved scaling, open research on **modular AI** may continue bridging capabilities. <br>- Different modules: retrieval, code execution, summarization, etc., each can be specialized and improved in isolation. |
| **Open Research vs. Closed Labs**    | - DSPy aspires to empower **open collaboration**, letting the community build new modules, inference strategies, and optimizers. <br>- Emphasis on reusability and portability—**no** enormous multi-billion-dollar training runs needed for progress.            |
| **Key Takeaways**                    | 1. Building “**compound systems**” can significantly boost accuracy, reliability, and interpretability. <br>2. **Natural language programming** (e.g., DSPy) decouples system design from brittle prompt engineering. <br>3. **Optimization** of prompts/demos is crucial for best performance.         |
| **Vision**                           | - A world where “**programming**” with LM modules is as straightforward as writing Python. <br>- Common shared libraries of “**predictors**,” “**optimizers**,” and “**module signatures**” accelerate advanced AI system development.                                                  |

---