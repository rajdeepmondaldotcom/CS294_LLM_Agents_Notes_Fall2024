
# Lecture 2

In this [lecture](https://youtu.be/RM6ZArd2nVc?si=NOERKGLm4Rto-0w6), we explored how **LM Agents** evolved from simpler text agents and rule-based systems, gaining powerful capabilities through **reasoning** (Chain of Thought) and **acting** (tool/environment interactions). Key breakthroughs like **React** show how interleaving thought and action creates more adaptive, human-like problem-solving. As tasks grow more complex, **long-term memory** and robust interfaces become essential, enabling agents to learn from mistakes and retain knowledge across sessions. Future research will focus on **training**, **interfaces**, **robustness**, **human collaboration**, and **benchmarking**, pushing LM agents into real-world applications where reliability and sustained performance matter most.

---

## Definition of LM Agents

| **Topic** | **Notes**                                                                                                                         |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **LM Agents**                   | - Agents that leverage Large Language Models (LLMs) to perceive and act within an environment using natural language. <br>- Combine **reasoning** (internal thinking) and **acting** (interactions with external tools/environments). |

---

## What is an “Agent”?

| **Topic** | **Notes**                                                                                                                            |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **Definition of Agent**         | - Broadly, an **agent** is an intelligent system that interacts with an environment (physical, digital, or even human-based). <br>- **Intelligent** implies some capacity for decision-making or problem-solving—though definitions of “intelligence” vary. |
| **Environments**                | - Physical (robotic arms, self-driving cars) <br>- Digital (video games, internet interfaces, APIs) <br>- Human (conversational chatbots)       |

---

## Text Agents vs. LM Agents vs. Reasoning Agents

| **Topic** | **Notes**                                                                                                                                                                                            |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Text Agent**                  | - Exchanges information and actions purely in language (e.g., text-based games, chat interfaces). <br>- Historically rule-based, or trained via Reinforcement Learning (RL).                                 |
| **LM Agent**                    | - A **text agent** specifically powered by a **Large Language Model** (like GPT-3, GPT-4).                                                                                                                   |
| **Reasoning Agent**            | - An LM agent that includes **reasoning steps** (Chain of Thought, reflection) in its decision-making. <br>- Goes beyond simple text output by planning and iteratively refining.                              |

---

## Early Chatbots (ELIZA)

| **Topic** | **Notes**                                                                                                                                           |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ELIZA (1960s)**               | - Used simple rules to respond, often mirroring user statements. <br>- **Limitations:** Highly domain-specific rules, non-scalable, no deep “understanding” of context. |

---

## Rule-Based / RL Agents

| **Topic** | **Notes**                                                                                                                                                                         |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule-Based Systems**          | - Rigid, domain-specific rules. <br>- Not easily adaptable to new tasks.                                                                                                                    |
| **RL in Text Environments**     | - Agents learn by maximizing reward in text-based settings (e.g., text games). <br>- Often requires extensive training steps and carefully designed reward signals.                         |
| **Pre-LLM Era**                 | - Before LLMs, rule-based systems and reinforcement learning approaches were common for text agents.                                                                                        |

---

## LM Agents and Reasoning

| **Topic** | **Notes**                                                                                                                                                                                  |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Next-Token Prediction**       | - LLMs (e.g., GPT-3) are trained on massive corpora, enabling **zero/few-shot in-context learning**.                                                                                                 |
| **Challenges in QA**           | 1. **Complex Reasoning** (multi-step arithmetic) <br>2. **Missing Knowledge** (post-training world events) <br>3. **External Computation** (large numbers, specialized tasks)                        |
| **Solutions**                   | - **Chain of Thought (CoT)** for multi-step reasoning. <br>- **Retrieval-Augmented Generation** for up-to-date info. <br>- **Tool Use** (external APIs, calculators, code execution) to handle specialized tasks. |

---

## Chain of Thought & Tool Use

| **Topic** | **Notes**                                                                                                                                               |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Chain of Thought**            | - LM generates intermediate reasoning (“thoughts”) before producing the final answer.                                                                            |
| **Tool Use**                    | - Embeds special tokens/calls to external resources (calculators, web search, weather APIs). <br>- Requires careful prompt formatting to interleave reasoning + tool actions.                           |
| **Task Diversity**              | - Different tasks (knowledge retrieval, math, current data) may require multiple tools and reasoning steps.                                                      |

---

## React Paradigm

| **Topic** | **Notes**                                                                                                                                      |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| **React = REAsoning + ACTing**  | - Agents use language to **think** (internal chain of thought) and produce **actions** (tool/API calls).                                                                 |
| **Example**                     | - Checking market caps of companies via web search: step-by-step refinement, parsing new info, adapting approach.                                                      |
| **Benefits & Generality**       | - **Benefits**: Acting helps gather new info; reasoning guides the next action. <br>- **Generality**: Works beyond Q&A (e.g., text-based video games, robotics with textual interfaces). |

---

## Long-Term Memory in Agents

| **Topic** | **Notes**                                                                                                                                                                                               |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Context Window Issue**        | - LLM context window is short-lived (“goldfish memory”); knowledge disappears after a session.                                                                                                                   |
| **Long-Term Memory**            | - Stores facts, experiences, or code for future reference (persisting beyond immediate context). <br>- **Reflection**: record past attempts, errors, or successes.                                               |
| **Examples**                    | - **Voyager** in Minecraft: remembers “skills” (code snippets) it learns. <br>- **Generative Agents**: diaries/logs of daily experiences—revisit episodic memory to inform new actions.                           |
| **Ways to “Learn”**             | 1. Updating LLM **parameters** (fine-tuning). <br>2. Recording knowledge in an **external memory** (retrievable text or code).                                                                                    |

---

## 10. Symbolic AI, Deep RL, and LM Agents

| **Topic** | **Notes**                                                                                                                                                         |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Symbolic AI**                 | - Early approach using logic/rules for agent decisions, often very domain-specific.                                                                                                                              |
| **Deep RL**                     | - Learns policy from environment reward signals (AlphaGo, Atari). Typically requires large-scale training.                                                                                                       |
| **LM Agents**                   | - Use **language** as the intermediate representation. Bridges symbolic and neural approaches. <br>- Minimizes domain-specific engineering. <br>- Supports **infinite** or open-ended internal reasoning. |

---

## New Applications (Digital Automation, Web Interaction)

| **Topic** | **Notes**                                                                                                                                                                                                 |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Digital Automation**          | - Agents handle tasks like reimbursements, paper reviews, large-scale code maintenance.                                                                                                                            |
| **Web Interaction**             | - **WebShop**: Agents browse e-commerce sites, refine searches, choose products. <br>- Agents fill forms, handle customer service, or complete any web-based workflow.                                            |
| **Software Engineering**        | - E.g., “SubMIT” tasks: agent navigates GitHub repos, runs unit tests, debugs/fixes issues.                                                                                                                        |
| **Scientific Discovery**        | - Agents propose new chemical structures, run code to analyze data, pass suggestions to real-world labs for synthesis.                                                                                             |

---

## Challenges & Future Directions

| **Topic** | **Notes**                                                                                                                                                                                                                                |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Training Specialized LM Agents**  | - Current LLMs weren’t explicitly trained to be “agents.” <br>- **Self-generated data** (agent rollouts) could help fine-tune or instruct models on reasoning/action traces.                                                                                           |
| **Interface & Environment Design** | - Better “action space” or custom commands for agents (e.g., specialized file-search commands). <br>- Human-Computer Interface research adapted to LMs (giving LMs multiple results at once, not line-by-line).                                                            |
| **Robustness & Reliability**       | - Real-world tasks often require **consistent** success, not just “pass@K.” <br>- Mistakes can be costly in customer service or critical applications. <br>- Agents must handle multi-turn interactions with partial/conflicting info.                                       |
| **Human Collaboration**            | - Agents frequently partner with humans to clarify instructions, gather domain info, or confirm solutions. <br>- Multi-step dialogues with real or simulated humans (e.g., flight changes, debugging).                                                                   |
| **Benchmarking**                   | - Need **new metrics** for reliability, consistency, and interactive success rather than single-pass performance. <br>- **ToolBench** / **TaskBench**: Evaluate collaboration, partial info handling, correctness across repeated attempts.                              |

---