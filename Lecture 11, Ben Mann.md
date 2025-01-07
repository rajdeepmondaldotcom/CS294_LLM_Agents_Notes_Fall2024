# Lecture 11

In this [lecture](https://www.youtube.com/live/6y2AnWol7oo?si=RFa8bTFA4LJb6opW) Anthropic’s **Ben Mann** highlights the mounting importance of **AI safety** as capabilities grow—from **simple coding agents** to future systems that could rival the best experts. By framing a **Responsible Scaling Policy** with “AI Safety Levels” (ASL-1 to ASL-4/5), Anthropic aims to systematically contain and vet new models before deployment. The demos of **computer-use** agents show how LLMs can already manipulate files, apps, and code, underscoring the potential for **misuse** if not rigorously sandboxed. Looking ahead, Anthropic envisions **multi-layer safety measures**, robust **measurement** (benchmarks), and **scalable governance** as essential to ensuring that advanced agents remain beneficial rather than dangerous.

---

## Introduction

| **Topic**        | **Notes**                                                                                                                                                                                                                                           |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Anthropic’s Background**            | - **Ben Mann**: Co-founder of Anthropic; previously at OpenAI, co-author on GPT-3 paper. <br>- Company founded in 2021. <br>- Focus on **transformer circuits** (mechanistic understanding) & **safe, commercial models** (Claude).                                                               |
| **Claude Launch & Adoption**          | - Multiple versions released (Claude, Claude 2, etc.). <br>- Key emphasis on **AI safety** and thorough testing prior to deployment.                                                                                                                                                                  |

---

## Measurement & Elicitation in AI

| **Topic**                      | **Notes**                                                                                                                                                                                                                                                                                        |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Why Measurement Matters**                          | - Hard to ensure safety if you can’t **measure capabilities and behaviors** accurately. <br>- “Elicitation”: The process of prompting to access latent abilities (e.g., chain-of-thought). <br>- Small changes (like “think step by step”) can yield dramatically different model outputs, thus complicating safety evaluations.                                |
| **Agent Context**                                    | - With agent loops, AI can autonomously **execute tasks in the real world**—coding, buying/selling, controlling browsers, etc. <br>- More powerful models → potential for more far-reaching actions (e.g., advanced cybersecurity capabilities).                                                                                                    |
| **Benchmark Leapfrogging**                           | - AI models jump in performance quickly on new benchmarks. <br>- Hard to create robust tests that scale with future capabilities.                                                                                                                                                                                                                |
| **Chain-of-Thought & AP** (Anthropic Perspective)    | - *Chain-of-thought prompting* reveals hidden reasoning steps. <br>- “Conversation tuning” or “dialog-style” drastically improved usability and *elicitation* of advanced reasoning from the same model.                                                                                                                                        |

---

## AI Capabilities, Scaling & Safety

| **Topic**                   | **Notes**                                                                                                                                                                                                                                                                |
|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scaling Compute → More Capabilities**           | - Straight line from prior “scaling laws” to future expansions in model size & compute. <br>- **GPT-2** ~ “Preschooler,” **GPT-3** ~ “Elementary,” **GPT-4** ~ “High-school.” Next gen could surpass *expert researchers.*                                                                                              |
| **Anthropic’s Theory of Change**                  | - As compute and data scale, model capabilities rise. <br>- Must ensure they are “**safe and beneficial** for everyone” at each step.                                                                                                                                              |
| **Demo: Coding with Claude 3.5 Sonnet**           | - Agent-driven code edits & testing. <br>- Tools (e.g., file edits, running tests) revolve in a loop → *faster iteration.* <br>- Concrete example: AI fixes bugs, runs unit tests, re-checks.                                                                                                                             |
| **Agents & Sandbox**                               | - Agents potentially do tasks like scheduling, booking, or advanced code generation. <br>- Must remain *sandboxed* (e.g., separate VM, restricted environment) until we have robust safety.                                                                                                                              |

---

## Responsible Scaling Policy (RSP) & AI Safety Levels

| **Topic**            | **Notes**                                                                                                                                                                                                                                                                                     |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Inspiration from Biosafety**            | - BSL (biosafety levels) as analogy for AI safety. <br>- A structured approach: define hazard levels & containment.                                                                                                                                                                                                                           |
| **ASL Overview**                          | - **ASL-1**: Low risk. e.g., older small LMs. <br>- **ASL-2**: Frontier models today (Claude 3.5, GPT-4) with possibly dangerous but *limited* potential. <br>- **ASL-3**: Models with significant advanced capabilities (e.g., state-of-the-art cybersecurity or autonomous replication). <br>- **ASL-4/5**: Even more advanced, surpassing best human experts. |
| **Requirement for Deploying Next ASL**    | - Must have specific **safeguards** before building or releasing more capable models. <br>- E.g., a “6-month hold” after training to test and evaluate model. <br>- *Goal:* “tie our own hands” so we don’t push unsafe capabilities prematurely.                                                                                       |
| **Possible Catastrophic Risk**            | - Models could replicate, accumulate resources, override oversight. <br>- “Evil Clippy” scenario: a low-prob sampling of “break out” -> self identifies as malicious.                                                                                                                                                                            |
| **Current Models**                        | - Anthropic sees Claude ~ near **ASL-2** (safe enough with strong policies). <br>- Next generation might push the boundary to ASL-3 → triggers stricter protocols.                                                                                                                                                                              |

---

## Agent Demos: Computer Use

| **Topic**                     | **Notes**                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Anthropic’s Computer Use**                        | - Secure sandbox for Claude controlling a **Mac**. <br>- Tools: open apps, move mouse, type keystrokes, take screenshots. <br>- State-of-the-art on *OSWorld*, though second place on accessibility-tree version.                                                                                                                                    |
| **Security Concerns**                               | - Model might see “hidden instructions” (white text on white background) telling it to do malicious things. <br>- Potential for credential exfiltration or manipulations. <br>- Must do **defense in depth**: sandbox the environment, system prompts, babysitter models (“Swiss cheese model”).                                                    |
| **APIs & Tools**                                    | - Tools are invoked by the model (call to “moveMouse,” “typeKey,” etc.). <br>- Model sees screenshots, decides next steps. <br>- Combine with advanced code checks to keep environment locked down.                                                                                                                                                   |
| **Future**                                          | - Possibly hours/days-long tasks autonomously. <br>- Emphasis on *sandboxing + advanced oversight* to ensure no unauthorized real-world actions.                                                                                                                                                                                                   |

---

## Scalable Governance & Benchmarks

| **Topic**                | **Notes**                                                                                                                                                                                                                                                                       |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Benchmarks for Agents**                     | - *SWE-bench*: Code generation, verified solutions. <br>- *OSWorld*: Multi-step tasks in simulated OS environment. <br>- Need real-world-like tasks but remain reproducible & safe.                                                                                                                                              |
| **Role of Public Accountability**              | - Anthropic’s **Long-Term Benefit Trust**: Governance structure so the company can’t ignore safety. <br>- *Similar to nonprofits or academic labs.*                                                                                                                                                                             |
| **Policy Influence**                           | - RSP framework influenced other labs (OpenAI “responsible deployment,” Google, etc.). <br>- Forward path: Continue to refine definitions, e.g., when do we cross from ASL-2 to ASL-3?                                                                                                                                           |
| **Delays, Pauses, & Forecasting**             | - If model capability outstrips safety infrastructure, labs may **pause**. <br>- Real possibility that “safety catch-up” might create a gap in new model releases.                                                                                                                                                                |

---
