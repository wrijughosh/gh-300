# Responsible AI Principles

GitHub Copilot is developed by GitHub and powered by OpenAI models. Both GitHub and Microsoft are committed to building AI systems following established Responsible AI principles.

---

## Microsoft's Six Responsible AI Principles

### 1. Fairness
AI systems should treat all people fairly and avoid affecting similarly situated groups of people in different ways.

- Copilot is trained on a diverse corpus of public code to reduce systemic bias.
- Output should be evaluated for fairness when used in contexts that affect people (e.g., hiring algorithms, access control).

### 2. Reliability and Safety
AI systems should perform reliably and safely, and behave as designed even in unexpected situations.

- Copilot includes safeguards to prevent the generation of malicious code patterns.
- Developers must test suggestions before deploying to ensure runtime safety.

### 3. Privacy and Security
AI systems should respect privacy and maintain data security.

- Copilot for Business and Enterprise do not use your code snippets to train the model by default.
- Prompts and completions are protected under GitHub's privacy policies.
- See [Data Handling and Flow](../03-data-architecture/data-handling-flow.md) for more.

### 4. Inclusiveness
AI systems should empower everyone, including people with disabilities.

- Copilot is available across editors and platforms to reach the widest audience.
- Suggestions should be reviewed to avoid reinforcing exclusionary coding patterns.

### 5. Transparency
AI systems should be understandable, and people should know when they are interacting with AI.

- GitHub clearly marks Copilot suggestions as AI-generated.
- GitHub publishes documentation about data usage, model training, and content filtering.

### 6. Accountability
People should be accountable for AI systems.

- Developers are responsible for the code they accept and ship—even if originally suggested by Copilot.
- Organizations can configure policies to limit what Copilot can do.

---

## How These Principles Apply to Copilot

| Principle | Copilot Application |
|---|---|
| Fairness | Diversity in training corpus, content filtering for bias |
| Reliability | Proxy filtering, output testing requirements |
| Privacy | No training on Business/Enterprise code by default |
| Inclusiveness | Multi-editor support, accessibility considerations |
| Transparency | Suggestions labeled as AI, public documentation |
| Accountability | Developer reviews suggestions; org policies configurable |

---

## Key Takeaways

- Responsible AI is a shared responsibility between the AI provider (GitHub/Microsoft), the organization, and individual developers.
- The six principles—Fairness, Reliability, Privacy, Inclusiveness, Transparency, Accountability—form the foundation of how GitHub Copilot is built and maintained.
- Being a responsible Copilot user means understanding these principles, applying them when reviewing suggestions, and escalating concerns appropriately.

---

[← Back to Responsible AI](README.md)
