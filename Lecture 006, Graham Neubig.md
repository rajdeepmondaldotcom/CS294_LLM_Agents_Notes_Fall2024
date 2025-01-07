# Lecture 6

In this [lecture](https://www.youtube.com/live/f9L9Fkq-8K4?si=SloOlOjbXBqOKgJb), we explored how **autonomous coding agents** can go beyond simple autocomplete to handle larger software tasks—creating tests, editing files, running code, and pushing commits. While **coding LLMs** (like GPT, Claude) excel at code generation, true automation demands careful **file localization**, **planning**, and **error recovery** in a sandboxed environment to maintain **safety**. Benchmarks such as **S-Bench** or **Arcade** help measure performance, but code data leakage and the complexity of real dev workflows remain challenges. Future directions involve improving code-based LLMs, developing more robust agentic training for multi-step tasks, and establishing best practices for human-in-the-loop collaboration and safety protocols.

---

## Introduction

|**Topic**|**Notes**|
|---|---|
|**Why Software Development Agents?**|- Software increasingly underpins most industries (“software is eating the world”). - If **everyone** could quickly write or fix software, massive innovation would result. - Modern science prizes (e.g., Nobel) often involve major software contributions.|
|**Coding vs. Other Dev Tasks**|- Only **15%** of dev time is spent writing new code. - Remainder: bug fixing, testing, documentation, reviews, communication (~36%), and other tasks.|

---

## Levels of Automation in Software Development

|**Topic**|**Notes**|
|---|---|
|**Analogy to Self-Driving**|- Ranges from **no automation** → **conditional** → **high** automation.|
|**Software Automation Levels**|0: Fully manual. 1: **Smart autocompletion** (Copilot, Cursor). 2: Chat-based tools that refactor or produce code. 3: Task-level automation. 4: **High automation**—agents that complete entire dev tasks end-to-end.|
|**Autocomplete vs. Agent**|- **Autocomplete** (GitHub Copilot, Cursor) → helps generate next lines, but user still in control. - **Agent** → more autonomous (e.g., opening repos, editing, testing, pushing PRs).|

---

## Example: Autonomous Coding Agents

|**Topic**|**Notes**|
|---|---|
|**Open Hands**|- An open-source platform/agent that can autonomously open repos, create tests, install deps, run tests, commit/push code. - The user can then review a pull request.|
|**Autonomous Issue Resolution**|- Agents spot “FixMe” tags in GitHub issues → attempt solutions, open PRs with minimal user intervention.|
|**Productivity Impact**|- Example: GitHub Copilot study found devs with Copilot were **78%** more likely to finish tasks **56% faster**. - Suggests coding automation ~**doubles** coding velocity.|

---

## Evaluating & Benchmarking Coding Agents

|**Topic**|**Notes**|
|---|---|
|**Simple Coding Benchmarks**|- **HumanEval**, **MBPP**: from text prompt → code solution. Similar to “LeetCode” style tests.|
|**Beyond Simple Tasks**|- **CONALA**: Stack Overflow Q&A with real code libraries (numpy, pandas, etc.). - **Data Science Notebooks (Arcade)**: incremental, cell-by-cell generation.|
|**S-Bench**|- Real GitHub issues → generate pull requests (PR). Must read entire codebase, pass new tests. - Great for multi-file, real-world repository tasks.|
|**Limitations & Leakage**|- **Data leakage**: Many public repos included in LM training sets. - Scores on HumanEval or MBPP may be artificially inflated if the code was in model’s pre-training corpus.|
|**Other Benchmarks**|- **Live CodeBench**: can reveal overfitting on standard sets like HumanEval. - **Multimodal** (Design2Code): from website screenshot → front-end code.|

---

## Observation & Action Spaces in Coding Agents

|**Topic**|**Notes**|
|---|---|
|**Agent Needs**|1. Understand repo structure & read existing code. 2. Modify/generate new code. 3. Run code & debug.|
|**Coda Approach**|- Shifts from single-step tool calls to generating entire **programs** or **scripts** that run multiple steps at once. - More efficient than standard “tool usage” (one call per step).|
|**u?u Agent / Open Hands**|- Specialized commands for searching & editing files. - Example: “show file lines 405–409” → sees partial code segment. Then “edit lines 404–407” → modifies code snippet.|
|**Code Execution + Tools**|- Agents can run code, see error messages, and refine. - Example: For loops to systematically fix multiple lines or search multiple files.|

---

## Code-Specific Language Models

|**Topic**|**Notes**|
|---|---|
|**Pre-Training on Code**|- All major LMs (GPT, Claude, Gemini, LLaMA, etc.) now include **code** in training. - Some specialized sets (e.g., **Stack** for code) handle license filtering, different languages.|
|**Infilling**|- Essential for code editing: mask out a section, put the mask at the end, let model learn to fill.|
|**Long Context**|- Coding tasks frequently need large context (entire files). - **RoPE** and other position encoding tricks for extended context beyond training length.|
|**Context Strategies**|- Typical code autocompletion uses local context (current file, 20 recent files, etc.). - Agents may also gather entire repo structure or rely on search-based retrieval of relevant files/functions.|

---

## File Localization & Environment Scanning

|**Topic**|**Notes**|
|---|---|
|**The Challenge**|- Many coding tasks require fixing or adding code in **unknown** files. Issue descriptions rarely specify exact file paths.|
|**Approaches**|1. **User Disambiguation**: The user pre-specifies which files to edit. 2. **Search Tools**: Agents use keywords to find relevant code snippets. 3. **Repo Map**: Summaries of entire repo, hierarchical exploration of classes/functions.|
|**Retrieval-Augmented Code Gen**|- Embedding-based search for “similar code” or relevant docs. - Potentially merges retrieved docs (comments, usage examples) into prompt for better context.|
|**Unsolved Problems**|- Hard to perfectly match user’s intent. - Large repos → extensive searching needed. - Future: More advanced hierarchical scanning + summarization of relevant files.|

---

## Planning & Error Recovery

|**Topic**|**Notes**|
|---|---|
|**Hardcoded Pipelines**|- Some agent frameworks (e.g., Agent-LLess) have a strict multi-step pipeline: localize file, generate patches, run tests, pick best patch. - Simple, often effective but lacks flexibility (can’t do doc lookups, chat with user, etc.).|
|**LLM-Generated Plans**|- Agents can propose a plan (e.g., find bug → fix → retest → finalize). - Risk: the plan might be flawed; the agent must be able to revise it mid-process if new info arises.|
|**Error Handling**|- Agents run code, parse error messages, attempt new fixes. - Some LLMs get stuck in loops (repeating same fix). Others (Claude) try multiple angles. - **Better training** for robust error recovery is a big future direction.|

---

## Safety & Security Considerations

|**Topic**|**Notes**|
|---|---|
|**Potential Harm**|1. Unintentional damage (e.g., agent commits/pushes flawed code to main branch). 2. Intentional misuse (agents writing or exploiting vulnerabilities).|
|**Sandboxing**|- Run agent actions in a **Docker** container or restricted environment. - Minimizes system access, preventing wide-scale or malicious changes.|
|**Principle of Least Privilege**|- Limit agent’s credentials (GitHub tokens with partial repo access, read-only mode, etc.). - Prevents agent from making changes beyond scope.|
|**Auditing & Post-Hoc Checks**|- Evaluate each proposed action (e.g., static analysis, LLM-based vulnerability detection). - “Deny” unsafe actions or require explicit user confirmation.|

---

## Conclusion

|**Topic**|**Notes**|
|---|---|
|**Ongoing Challenges**|1. Building better **code LLMs** (multilingual, specialized, domain coverage). 2. More advanced **file localization** & environment scanning. 3. **Planning** & robust error recovery. 4. Maintaining **safety** with partial privileges and audits.|
|**Agentic Training**|- New training sets to teach LLMs multi-step agent behavior, planning, error handling.|
|**Human-in-the-Loop**|- Methods to combine user feedback mid-run. - No established benchmarks to measure “interactive agent + user collaboration.”|
|**Expanding Scope**|- Agents dealing with other software tasks (documentation, design specs, communication, etc.).|
|**Takeaway**|- Current coding automation is **already** highly useful (e.g., Copilot). - Next 1–2 years: more advanced “coding agents” likely to handle bigger tasks reliably.|

---
