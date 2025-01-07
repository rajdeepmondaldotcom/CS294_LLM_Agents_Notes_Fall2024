
# Lecture 4, Burak Gokturk

In this [lecture](https://www.youtube.com/watch?v=Sy1psHS3w3I), we examined the **rapid evolution of AI**—from early skepticism about neural networks to today’s **powerful large language models**. Key breakthroughs include **parallel computing**, **transformer architectures**, and **massive datasets** for pre-training. We also discussed how **enterprises** are integrating LLMs with **search** to ensure up-to-date, factual results, and are increasingly using **function calling** to enable real-world tasks. With **costs** dropping and **capabilities** rising, the future of AI promises unprecedented growth, requiring ongoing innovation in **grounding**, **factual accuracy**, and **efficient customization** of models.


---

## Introduction & Overview

| **Topic**         | **Notes**                                                                                                                                                                                                                             |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Lecture Context**                    | - The lecture gives an overview of the current trends and advancements in **Artificial Intelligence (AI)** and **Large Language Models (LLMs)**. <br>- Focuses on **enterprise adoption**, **model customization**, **function calling**, and **search integration**. |
| **Shifts in AI Adoption**              | - AI adoption in enterprises has accelerated significantly, especially after **ChatGPT**’s launch in late 2022. <br>- More companies and developers are leveraging large models without requiring deep AI expertise.                                                      |

---

## Historical Context: Neural Nets & LLM Emergence

| **Topic** | **Notes**                                                                                                                                                                                                                                |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Early Skepticism**            | - Neural networks were once considered “outdated” compared to Support Vector Machines or Decision Trees. <br>- Limited data (e.g., ~50 patient CT images) made training slow and gave poor results in the past.                                                                     |
| **Key Turning Points**          | 1. **Parallelization** on GPUs/TPUs made training large networks feasible. <br>2. **Access to massive datasets** from the web and books. <br>3. **Transformer architectures** greatly improved performance in language tasks.                                                           |
| **Rise of LLMs**                | - Large-scale next-token prediction via “masking” (e.g., fill-in-the-blanks tasks) created huge training corpora. <br>- Result: LLMs can now handle various tasks in zero/few-shot settings.                                                                                            |

---

## Generative AI & ChatGPT Breakthrough

| **Topic**      | **Notes**                                                                                                                                                                                                     |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **November 2022 Milestone**         | - **ChatGPT** public release: changed global perception about AI capabilities. <br>- Demonstrated LLMs’ utility in coherent text generation for general users, not just researchers.                                   |
| **Generative Capabilities**         | - LLMs can generate text, code, images (with multimodal models), or other outputs. <br>- Surpassed older methods (like older speech/image models) in versatility and scale of tasks.                                    |
| **Acceleration & Surprises**        | - Many researchers expected this level of AI progress in 100 years—reality: ~15 years. <br>- Enterprise excitement soared, leading to a surge in AI pilot projects and product integrations.                              |

---

## Performance Gains in Image & Speech

| **Topic** | **Notes**                                                                                                                                                                     |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ImageNet & Beyond**           | - Image classification accuracy rose from ~50% in 2011 to over 90% by 2022. <br>- Achieved near “human-level” performance with large neural networks.                                                                       |
| **Speech Recognition**          | - Error rates dropped dramatically (e.g., from ~13% in 2016 to ~2.5% in a few years). <br>- Google, OpenAI, Anthropic models perform near-human level on many speech tasks.                                                  |
| **Generative AI Two-Way**       | - AI can now **understand** images/speech and also **create** them (e.g., DALL·E for images, text-to-speech tools).                                                                                                           |

---

## LLM Training Process: Masking & Next-Token Prediction

| **Topic**       | **Notes**                                                                                                                                                                                                     |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Masking / Fill-in-the-Blanks**      | - Training technique: mask certain words in a sentence and predict them. <br>- Massive text corpora (web, books) create nearly infinite labeled data for LLMs.                                                                 |
| **Versatility of LLMs**               | - Produce text styles ranging from technical explanations to casual conversation. <br>- Handle Q&A, summarization, code writing, and beyond.                                                                                 |
| **Challenges & Solutions**            | - **Fine-tuning** large models for specific tasks can be resource-intensive. <br>- **Reinforcement Learning from Human Feedback (RLHF)** or expert-labeled data used to refine model outputs.                               |

---

## Reinforcement Learning & Fine-Tuning

| **Topic** | **Notes**                                                                                                                                                                                                |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Supervised Fine-Tuning**      | - Collect prompts & expert responses → train to match these “gold” answers. <br>- Effective but requires **large** curated datasets.                                                                                 |
| **Reinforcement Learning from Human Feedback (RLHF)** | - Model generates multiple responses; humans (or AI “raters”) up/downvote them. <br>- Faster than gathering expert-labeled data for every single prompt. <br>- Feeds into a **reward model** to improve output quality.                           |
| **Trade-Offs**                  | - **Expert-labeled data** yields high accuracy but is expensive and slow. <br>- **Human feedback** is cheaper but may be less precise.                                                                             |

---

## Google Gemini & Multi-Modal Models

| **Topic** | **Notes**                                                                                                                                                                  |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Gemini Overview**             | - Google’s multi-modal model, handles text, images, audio, and video. <br>- Large context window (testing up to **10 million tokens**).                                                                                    |
| **Potential Impact**            | - Could push boundaries on **input size** (entire documents, videos). <br>- Raises questions about whether huge context windows might replace traditional **search** or indexing algorithms.                                |
| **Needle in the Haystack Test** | - Benchmark for large contexts: drop a small “needle” (snippet) into massive text → see if the model can retrieve it. <br>- Used to measure if LLMs truly can handle large, unstructured data.                             |

---

## Trends in Enterprises

| **Topic**     | **Notes**                                                                                                                                                                                                 |
|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rapid AI Adoption**               | - Post-ChatGPT, enterprises are eager to pilot AI features. <br>- AI usage grew from niche to mainstream in months, not years.                                                                                   |
| **Reduced Need for Big Datasets**   | - **Large pre-trained models** reduce the data requirement: minimal fine-tuning can adapt them to enterprise tasks. <br>- Startups and even middle/high school students can build AI apps using existing LLMs.  |
| **Developer Democratization**       | - Shift from **AI experts** to **all developers**: modern LLM tools require less specialized knowledge.                                                                                                           |
| **General vs. Domain-Specific**     | - Rapid improvement in **base models** sometimes outpaces domain-specific models. <br>- Still an open research area: how to efficiently create or fine-tune specialized LLMs for healthcare, finance, etc.         |

---

## Cost & Latency Trends

| **Topic** | **Notes**                                                                                                                                                                                |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Sparse vs. Dense Models**     | - Move from fully “dense” Transformer networks to more “sparse” paths. <br>- **Sparse** inference reduces latency and cost by only activating parts of the model.                                  |
| **API Cost Approaches Zero**    | - Hosting models at scale has become cheaper, though hardware demands remain high. <br>- Open-source vs. commercial hosting can be surprisingly similar in cost once you factor in hardware & maintenance. |

---

## Distillation & Domain-Specific Models

| **Topic** | **Notes**                                                                                                                                                                                                                        |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Model Distillation**          | - **Teacher–Student** setup: a large model (teacher) labels data, smaller model (student) trains to replicate teacher’s outputs. <br>- Eliminates need for extensive human labeling if teacher is sufficiently accurate.              |
| **Temperature & Soft Labels**   | - Using a “temperature” parameter can smooth out teacher predictions, providing “soft” probabilities for the student to learn from.                                                                                                        |
| **Benefit**                     | - Drastically reduces **latency** and **cost** for specific tasks—ideal for enterprise who only need limited domain coverage.                                                                                                              |

---

## Search & LLM Integration (Grounding)

| **Topic** | **Notes**                                                                                                                                                                                                     |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Why Combine Search + LLM?**   | 1. **Current Data**: LLMs train on past data; search provides up-to-date info. <br>2. **Factual Accuracy**: LLMs can hallucinate; search can ground or verify answers. <br>3. **Citations**: LLMs alone can’t pinpoint sources, but search can.                   |
| **RAG / Retrieval-Augmented**   | - Common pipeline: (1) Convert user query → (2) Search engine retrieves relevant docs → (3) LLM merges docs + prompt for final output. <br>- Often referred to as **RAG** (Retrieval-Augmented Generation).                                                    |
| **User Experience**             | - Enterprises want **source citations** & reliable references. <br>- In mission-critical applications (healthcare, finance) hallucinations are unacceptable, so verified search results are crucial.                                                          |

---

## Function Calling & Extensions

| **Topic**     | **Notes**                                                                                                                                                                                              |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Purpose**                         | - Allows LLMs to take **real-world actions** (booking flights, editing databases, retrieving bills). <br>- LLM must recognize **“I can’t do this alone”** and call the appropriate function/tool (like an “Expedia function” for flight booking).          |
| **Implementation Steps**            | 1. **Define Functions** (extensions) for specific tasks. <br>2. LLM is trained or prompted to call these when needed. <br>3. LLM decodes which function to use based on user request and its own capability gaps.                                      |
| **Challenges**                      | - Must handle an ever-growing “library” of extensions. <br>- LLM must pick **which** extension to call and **when** to do so.                                                                                                                           |
| **Potential Applications**          | - Structured data retrieval, real-time flight info, e-commerce purchases, updating enterprise CRM records, etc.                                                                                                                                       |

---

## Tools & Ecosystem (Prompt Management, Evaluation)

| **Topic** | **Notes**                                                                                                                                                                                                             |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Prompt Management**           | - Systematic versioning of prompts (tracking changes, storing best prompts). <br>- Converting prompts from one model format to another.                                                                                                                                   |
| **Evaluation Tools**            | - **Side-by-side** model comparisons: run multiple LLMs on same prompt and evaluate. <br>- Increasingly, large models themselves are used to **judge** outputs (auto-evaluation).                                                                                          |
| **Enterprise Requirements**     | - Reliability (99.999% uptime), security, flexible hardware (GPU vs. TPU). <br>- Ability to **compare** multiple LLMs in real-time and pick the best for the use case.                                                                                                  |

---

## Future Outlook & Final Remarks

| **Topic** | **Notes**                                                                                                                                                                      |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Growth & Speed**              | - AI usage is growing at an **unprecedented** rate (tens of thousands of enterprises adopting features in weeks). <br>- API calls for AI services have multiplied exponentially in less than a year.                               |
| **Interdisciplinary Importance**| - Advisable to combine AI with other fields (sciences, humanities, arts) to spur creativity.                                                                                                                                    |
| **Ongoing Transformations**     | - Search, function calling, and multi-modal expansions will keep pushing LLM boundaries. <br>- Factuality vs. Creativity trade-offs will drive next-gen RLHF and grounding research.                                             |
| **Career & Research Tips**      | - Explore specialized or “custom domain” LLMs, bridging AI with healthcare, finance, or creative industries. <br>- Keep an eye on **low-latency** solutions (distilled or parameter-efficient approaches).                          |

---