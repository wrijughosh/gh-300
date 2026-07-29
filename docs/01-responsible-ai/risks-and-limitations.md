# Risks and Limitations of Generative AI Tools

Understanding the risks and limitations of Generative AI is essential for using GitHub Copilot responsibly and safely.

---

## What is Generative AI?

Generative AI refers to machine learning models that generate new content—text, code, images—based on patterns learned from large training datasets. GitHub Copilot uses large language models (LLMs) trained primarily on publicly available code and text.

---

## Core Risks

### 1. Hallucination
LLMs can generate plausible-sounding but factually incorrect or non-existent outputs. In code, this can manifest as:
- References to APIs or libraries that do not exist
- Invented function signatures that look correct but fail at runtime
- Incorrect logic that compiles successfully but produces wrong results

**Mitigation:** Always test generated code. Never assume output is correct just because it looks valid.

### 2. Bias
AI models reflect the biases present in their training data. This can result in:
- Code that favors certain programming styles or paradigms without good reason
- Generated comments or documentation using non-inclusive language
- Subtler algorithmic biases in business logic (e.g., demographic assumptions)

**Mitigation:** Review all suggestions critically. Supplement code reviews with bias awareness.

### 3. Security Vulnerabilities
Copilot may suggest code that is technically correct but insecure:
- Hard-coded credentials
- SQL injection vulnerabilities
- Insecure cryptographic choices
- Improper input validation

**Mitigation:** Use Copilot security features, code scanning tools (e.g., CodeQL), and security-focused reviews.

### 4. License and Copyright Issues
Copilot is trained on public code that may include various open-source licenses. Suggestions may:
- Resemble or reproduce code from licensed sources
- Carry implicit licensing obligations
- Infringe on copyrights if used without review

**Mitigation:** Enable the "Suggestions matching public code" filter. Review legal context before using large code blocks.

### 5. Over-Reliance
Developers who over-rely on Copilot may:
- Miss learning opportunities
- Accept incorrect suggestions without understanding
- Lose confidence in their own skills over time
- Ship bugs they don't understand

**Mitigation:** Use Copilot as a collaborator, not a replacement. Understand what you accept.

### 6. Outdated Knowledge
LLMs have a training cutoff date. Copilot may:
- Suggest deprecated APIs
- Miss recent security patches or best practices
- Reference outdated library versions

**Mitigation:** Verify suggestions against current documentation.

---

## Limitations of LLMs

| Limitation | Description |
|---|---|
| No true understanding | LLMs predict tokens statistically; they do not "understand" code |
| Context window limits | Copilot has a finite context window; large codebases exceed it |
| Non-determinism | Same prompt can produce different outputs each time |
| No long-term memory | Each session starts fresh (unless using features like Copilot Memory) |
| No real-world grounding | Cannot access live data, APIs, or documentation by default |
| Training data cutoff | Knowledge is frozen at a point in time |

---

## Key Takeaways

- Generative AI tools like Copilot are powerful assistants, but they are not infallible.
- Hallucination, bias, security risks, and over-reliance are the primary risks to understand.
- Mitigation requires a combination of tool configuration, human review, and testing practices.

---

[← Back to Responsible AI](README.md)
