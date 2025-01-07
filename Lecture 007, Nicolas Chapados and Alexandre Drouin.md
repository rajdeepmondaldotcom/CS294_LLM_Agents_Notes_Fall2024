# Lecture 7

In this [lecture](https://www.youtube.com/live/-yf-e-9FvOc?si=lVAR1jZfwAqWSjg-) we explored how Enterprise **AI agents** stand to dramatically streamline everyday workplace tasks by combining **LLM-driven autonomy** with robust tools for **web navigation** and **API integration**. The **TapeAgents** framework introduces a *shared log (tape)* that simplifies debugging and optimization, while **WorkArena** and other benchmarks show that web agents still face substantial reliability and planning hurdles. Despite present limitations, the **potential** for AI agents to transform knowledge work—by automating low-level, high-frequency processes and partnering with humans in more complex workflows—is enormous.

---

## Introduction

| **Topic**              | **Notes**                                                                                                                                                                                                                                |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ServiceNow & Workflows**                 | - ServiceNow: a global company (25,000 employees) focused on **enterprise workflow automation** (IT, HR, customer support). <br>- Provides a **platform** + developer tools for building new workflows. <br>- Growing interest in using **AI agents** to automate tasks.                |
| **Motivating Example**                      | - User spills coffee on laptop → opens an IT help desk ticket. <br>- Currently, a *human agent* does manual tasks (ordering, approvals, resolution notes). <br>- AI agents can automate parts of these **low-level, repetitive** workflows.                                             |

---

## Defining LLM Agents & Enterprise Workflows

| **Topic**       | **Notes**                                                                                                                                                                                                                                                      |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **LLM Agent Definition**             | - **Autonomy**: Plans actions, interacts with environment, can receive feedback, and iterates to achieve goals. <br>- Different from older RL-based agents (narrow scope, e.g., game playing). <br>- LLMs see broad internet data (e.g., instructions for Office, SAP, etc.). |
| **Two Types of Agents**              | 1. **API-Calling Agents:** Access formal, text-based endpoints or tools. <br>2. **Web Agents:** Interact with websites like humans (clicking, form-filling, multi-page navigation).                                                                                      |
| **Enterprise Automation**            | - Many tasks are *already* automated for high-volume, high-value flows. <br>- **LLM agents** can address *low-volume, low-value tasks* that are *too unique* for scripted automation (e.g., scheduling a 15-person meeting across companies, filling custom forms, etc.).   |
| **Web Agent Demo**                   | - Example: Using a web agent to find the route from NVIDIA HQ to GTC conference location. <br>- The agent consults Google Maps, clarifies user input, replans, and eventually finds directions.                                                                             |

---

## API Agents & TapeAgents Framework

| **Topic**                 | **Notes**                                                                                                                                                                                                                                                                                                      |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **API Agent Architecture**                      | - LLM → Takes input, emits actions → Environment (tools/APIs) → Observations → LLM updates internal state. <br>- Agents can store short-term memory and use techniques like **ReAct** or chain-of-thought. <br>- Tools vary (code execution, web access, specialized APIs).                                              |
| **Need for a Framework**                       | - Building & debugging agents is complex (similar to coding ML from scratch vs. using PyTorch). <br>- Also need to optimize prompts, *fine-tune* LLMs for better agent performance. <br>- Existing frameworks focus on either software engineering or optimization, not both.                                             |
| **TapeAgents**                                  | - **Tape** = single log of *all thoughts/actions* from all agents and environment responses. <br>- Agents can read the tape (history) and produce new outputs; tapes can be reused for *prompt optimization* or *fine-tuning*. <br>- Open-sourced days before the lecture; includes concurrency, modular design.        |
| **Tape as Data**                                | - Rich structure: stores metadata, environment calls, agent internal monologues. <br>- **Enables debugging, auditing, or “student-distilled” agents** (fine-tuning a smaller model on the behavior of a larger one). <br>- Agents process tapes to refine prompts or **reduce inference cost** with a smaller LLM.      |
| **Case Study: Distilling Large Agent**          | - Target example: complex form-filling assistant for enterprise tasks. <br>- Big, expensive model (e.g., GPT-4-level) logs tapes of solutions → fine-tune an 8B param model. <br>- Achieves **similar “GREADTH”** (grounded, responsive, accurate, etc.) at **300× lower cost**.                                       |

---

## Web Agents & Benchmarks

| **Topic**         | **Notes**                                                                                                                                                                                                                                                                                                |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Web Agents**                          | - Agents that act in a browser (Playwright, Selenium, etc.) by clicking, typing, navigating. <br>- More *general* than API agents, since they can handle situations without formal endpoints.                                                                                                                     |
| **Challenges**                          | 1. **Situational Awareness**: Understanding large HTML or multiple pages. <br>2. **Long-Term Planning**: Possibly many navigations away from the start page. <br>3. **Correct Execution**: Must not hallucinate buttons or controls, must handle changing UIs.                                                                                      |
| **Basic Web Agent Example**             | - Prompt with: (a) task instruction, (b) HTML or site context, (c) actions it can perform. <br>- LLM outputs which action to take → Python script executes in the browser.                                                                                                                                         |
| **Benchmarks for Web Agents**           | - *MiniWoB* (simple tasks like fill text box, submit). <br>- *Trace-based Datasets*: Use gold human traces, but can be limiting. <br>- *Live Benchmarks*: Evaluate final outcomes on real/hosted sites.                                                                                                           |
| **WorkArena**                           | - A **ServiceNow-based** remote benchmark with 600 tasks (3 levels). <br>- Tasks reflect **real enterprise workflows** (e.g., reorder low-stock items, read dashboards, knowledge base queries). <br>- Humans ~94% success, but best agent ~42.7% on easiest tasks, often 0% on complex tasks.                                                        |
| **BrowserGym & AgentLab**              | - **BrowserGym**: Standardized environment for web agent tasks (HTML, actions, local or remote hosting). Consolidates major web benchmarks. <br>- **AgentLab**: Toolbox for building web agents, debugging, profiling, and reproducibility (AgentXRay). <br>- Goal: unify observation/action spaces and share large sets of traces for community improvement. |
| **Common Failure Cases**                | - Lack of exploration, hallucinated UI elements, incorrect syntax for actions. <br>- Need advanced retrieval, multi-agent collaboration, or specialized sub-agents.                                                                                                                                              |
| **Other Challenges**                    | 1. **Context Size & Relevancy**: Potentially thousands of tokens in HTML. <br>2. **Long-Term Plan**: Hard to foresee multi-step path. <br>3. **Learning & Adaptability**: On-the-fly fine-tuning or searching. <br>4. **Efficiency**: Agents can be slow if LLM calls are large. <br>5. **Safety**: Injection attacks, malicious page scripts.                          |

---

## Future of Agents in the Workplace

| **Topic**            | **Notes**                                                                                                                                                                                                                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Illustrative Future**                   | - Example: *Sandy* receives a ticket → Agents already partially solve it (tool for user permission fix, KB check). <br>- Sandy only reviews or approves steps. <br>- End game: Agents automatically handle most substeps, drastically reducing manual drudge work.                                                              |
| **Knowledge Work Impact**                 | - **O*NET Database**: US job descriptions + tasks. Agents could partially automate many knowledge-worker tasks. <br>- Adoption curve depends on *tech readiness*, *user acceptance*, *organizational factors*.                                                                                                               |
| **McKinsey Adoption Curves**              | - Generative AI, including agents, can see *significant uptake* in coming years. <br>- Many roles or tasks will be redefined, requiring reskilling or shifting responsibilities.                                                                                                                                               |
| **Human–Machine Collaboration**           | - Two patterns: **Centaur** (LLM handles big sub-tasks, human orchestrates) vs. **Cyborg** (continuous back-and-forth collaboration). <br>- Future HCI research will find the best UX to integrate agent intelligence with human oversight.                                                                                     |

---
