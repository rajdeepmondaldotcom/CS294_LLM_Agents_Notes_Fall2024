# Lecture 12

In this [lecture](https://www.youtube.com/live/QAgR4uQ15rc?si=r4Jl-M1w4qeW-VGu) Dawn Song underscores the **pressing need for safe and trustworthy AI agents**, especially as *Frontier AI* capabilities expand. She highlights two core challenges: **(1) Ensuring AI trustworthiness and alignment** (protecting user privacy, robustly resisting adversarial triggers, and building “secure by design” solutions), and **(2) Mitigating AI misuse** (e.g., more potent cyberattacks, large-scale social engineering). Current defenses are fragmented or easily bypassed by novel prompt injections or training-time data poisoning. Professor Song advocates a new push for **quantitative, formal safety** and an evidence-based AI policy framework. By systematically understanding risks, enacting robust technical defenses, and adopting “science-based” regulation, we can responsibly harness advanced AI while guarding against malicious exploitation.

---

## Introduction

| **Topic**    | **Notes**                                                                                                                                                                                                                                           |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Central Challenges**             | 1. AI’s powerful capabilities → *broad spectrum of risks* (misuse, malicious use, malfunctions, systemic risks). <br>2. Attackers target new technologies. <br>3. AI security \[protecting the system from attackers\] + AI safety \[protecting external environment from AI\].                                       |

---

## Trustworthiness and Alignment in AI

### Privacy and Data Leakage

| **Topic**                  | **Notes**                                                                                                                                                                                                                                                                                         |
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Privacy Threats**                              | - LLMs can memorize training data. Attackers (w/o model details) can query the model to extract **sensitive info** (credit cards, SSNs, personal data). <br>- Shown in Dawn Song’s group’s *Enron email dataset* experiment.                                                                                                                       |
| **Exposure Metric**                               | - Proposed measure for how memorized an LLM is (degree of data leakage).                                                                                                                                                                                                                                      |
| **Large LLMs**                                   | - Larger models → More capacity → *More memorization* risk. <br>- Attackers can prompt to reveal email addresses, system prompts, personally identifiable info.                                                                                                                                                |
| **Defenses**                                     | 1. **Differential Privacy (DP)**: Clipping gradients + noise → mitigates memorization. <br>2. *Data scrubbing*, *deduplication*, *machine unlearning*. <br>- *Trade-offs:* some utility/performance drop and overhead.                                                                                                                             |

### Robustness (Adversarial Examples)

| **Topic**       | **Notes**                                                                                                                                                                                                                                                                              |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Adversarial Examples**             | - Small perturbations to input cause **wrong predictions** with high confidence. <br>- Observed in *image classifiers*, *self-driving sign classification*, etc. <br>- Real-world (physical) *stop sign attacks* that remain robust across viewpoints.                                                                                  |
| **Adversarial Attacks on LLMs**      | - Attacks that break **safety alignment** (e.g., coaxing harmful/incorrect responses). <br>- *Decoding Trust* paper: LLM trustworthiness across many scenarios → LLMs vulnerable to adversarial prompts. <br>- *Universal prompt attacks* appended to user queries can produce disallowed outputs.                                                          |
| **Inference-time vs. Training-time** | - *Inference time*: “Adversarial examples,” “Jailbreak prompts.” <br>- *Training time (data poisoning)*: Poisoned data can embed a **backdoor** (trigger phrase causes malicious outputs). <br>- E.g., “current year 2024” triggers vulnerable code in a large LM, bypassing safety alignment.                                                                 |

### Agent-Specific Safety Concerns

| **Topic**                   | **Notes**                                                                                                                                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Complex Agent Stack**                           | - Users → LLM agent → Tools/Memory → Real actions. <br>- Agents can store credentials, manipulate environment. <br>- Raises questions: *Which role can cause harm?* Everyone (the user, the LLM, external attacker, etc.).                                                                                   |
| **Prompt Injection**                              | - Core vulnerability: Malicious instructions override system or user instructions. <br>- *Direct injection:* Attack user prompt. <br>- *Indirect injection:* Attack hidden data (e.g., resume text) containing “ignore previous instructions.” <br>- Similar to SQL injection in database security.                                                  |
| **Attack Surfaces**                               | - *Broad:* Malicious user inputs, RAG databases, external references, supply chain data. <br>- E.g., “AgentPoison” research: embedding vectors/backdoors in retrieval sets.                                                                                                                                     |
| **Defense Approaches**                            | - **Prompt-level**: detection (prompt filters) or prevention (restructuring prompts). <br>- **Model-level**: robustly train to follow privileged instructions over malicious ones. <br>- **System-level**: security architecture (least privilege, sandboxing, isolation).                                                                            |

### Limitations of Current Defenses

| **Topic** | **Notes**                                                                                                                                                                                                                                                                                                               |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Defensive Techniques**        | - Detection-based: scanning prompts, searching for suspicious patterns. <br>- Prevention-based: rewriting or encoding instructions. <br>- Full alignment methods: RLHF, Constitutional AI, input/output guardrails.                                                                                                                                                     |
| **Challenges**                  | - Attacks adapt. *None* of these are guaranteed effective vs. new, sophisticated adversaries. <br>- Defense can degrade model performance. <br>- Adversarial robustness remains an **unsolved** open problem.                                                                                                                                                             |
| **Call for More Research**      | - Need “adversarially robust alignment,” new frameworks for robust interpretability, secure by design. <br>- E.g., representation engineering to identify “activation directions” for controlling honesty. <br>- Eventually, *Secure-by-Construction* (formal verification) for certain symbolic components.                                                               |

---

## Mitigating Misuse of AI

### Dual-Use Threat: AI for Attacks

| **Topic**             | **Notes**                                                                                                                                                                                                                                     |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Misuse / Malicious Actors**              | - AI can be used for beneficial tasks or for *harm* (cyberattacks, disinformation). <br>- Example: Attackers use advanced LLM code generation to discover software vulnerabilities, craft advanced phishing, or produce deepfake.                                                            |
| **Cybersecurity Impact**                   | - *Frontier AI* changes how attackers + defenders operate. <br>- Attackers: use AI to hack, scale up social engineering. <br>- Defenders: might use AI for faster bug discovery or detection.                                                                                                 |

### Attackers vs. Defenders

| **Topic**          | **Notes**                                                                                                                                                                                                                                                                 |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Stages of Attacks**                   | - AI can assist at each step in the kill chain (recon, exploit dev, pivot, exfil). Some steps are easier than others.                                                                                                                                                                |
| **Attacks on Humans**                   | - Social engineering & phishing. *Humans are weakest link*. <br>- Deepfake calls or videos → trick employees. <br>- Scale + sophistication are surging with GenAI.                                                                                                                                 |
| **Defense Methods**                     | 1. **Reactive**: detect & block attacks (AI can help detect anomalies but attackers adapt). <br>2. **Bug-finding**: identify vulns before attacker; but patching is slow and incomplete. <br>3. **Secure-by-Construction**: formal verification for provably secure software.                                   |
| **Asymmetric Challenges**               | - Offense is easier: only needs 1 unpatched hole. <br>- Defense must fix *all* vulnerabilities. <br>- Attackers can tolerate high failure rates. <br>- Patching is slow.                                                                                                                                 |

### Net Impact on Cyber Landscape

| **Topic**                          | **Notes**                                                                                                                                                                                                                                                                 |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Near-Term Advantage**                                  | - “AI will help attackers more,” as Dawn Song’s group analysis shows. <br>- Systems are ill-prepared (lack robust defenses, slow patch cycles).                                                                                                                                    |
| **Lessons from Past**                                    | - Medical device security research → took 5 years for FDA to adopt guidance. <br>- Similar pattern: only after big attacks/damages do we see major security investments.                                                                                                                                                  |
| **Call to Action**                                       | - *Act now*, reduce arms race, build AI-driven defenses, preserve user trust, push for provably-secure, safe design.                                                                                                                                                                                                      |
| **Humans as Weak Link**                                  | - Need advanced AI to defend humans from advanced phishing/ deepfakes. <br>- Possibly “AI guardians” that intercept scam calls or suspicious messages.                                                                                                                                                                     |

---

## Path Toward Science & Evidence-Based AI Policy

### Fragmented Policy Landscape

| **Topic**            | **Notes**                                                                                                                                                                                                                                                       |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Proliferation of AI Bills**             | - ~120 AI bills at US federal level, ~600 at state level. <br>- Highly fragmented, differing approaches to risk prioritization.                                                                                                                                          |
| **Need for Cohesion**                     | - Without consistent standards, we risk suboptimal regulations. <br>- Potentially lost opportunities to prevent catastrophic outcomes.                                                                                                                                    |

### Proposed Science/Evidence-Based Approach

| **Topic**                     | **Notes**                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Core Principle**                                  | - AI policy must hinge on *scientific understanding* of risk + effective mitigations. <br>- Current knowledge is limited, so we must expand *evaluation, evidence gathering.*                                                                                                                                                                          |
| **Five Priorities**                                 | 1. **Comprehensive AI risk understanding**: Broad coverage, marginal risk approach. <br>2. **Increased transparency** in model design/training. <br>3. **Early detection & warning** (pre-deployment evaluation + post-deployment monitoring). <br>4. **Mitigation & defenses**: new solutions beyond standard alignment. <br>5. **Build trust & reduce fragmentation**. |
| **Blueprint for Future Policy**                     | - Create a “map” of future conditions (model capabilities, demonstrated harms) → recommended policy responses. <br>- Multi-stakeholder convenings, collaborative process.                                                                                                                                                                               |
| **Next Steps**                                      | - Over 200 institutions joined. Ongoing to refine framework, hold events, cultivate multi-stakeholder alignment. <br>- Info: *understanding-ai-safety.org*.                                                                                                                                                                                            |

---