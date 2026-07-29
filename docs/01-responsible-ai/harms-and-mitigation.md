# Potential Harms and Mitigation Strategies of AI Usage

GitHub Copilot, like all generative AI tools, can cause harm when used carelessly. This section identifies the main categories of potential harm and the mitigation strategies available to developers and organizations.

---

## Categories of Potential Harm

### 1. Security Harms
AI-generated code may introduce vulnerabilities:
- **Injection attacks** (SQL, command, LDAP)
- **Insecure deserialization**
- **Hard-coded secrets** (API keys, passwords)
- **Weak cryptography** (outdated algorithms, short key lengths)
- **Path traversal and directory exposure**
- **Cross-site scripting (XSS) in web code**

**Mitigation Strategies:**
- Enable GitHub Advanced Security (code scanning with CodeQL)
- Use secret scanning to detect accidentally committed secrets
- Perform security-focused code reviews on all AI-generated code
- Use [Copilot security improvement suggestions](../05-developer-productivity/testing-security.md)

---

### 2. Privacy Harms
Developers may unintentionally expose sensitive information:
- Sharing PII (Personally Identifiable Information) in prompts
- Generating code that mishandles user data
- Leaking internal business logic through prompts

**Mitigation Strategies:**
- Never include raw sensitive data in prompts; use placeholders
- Configure [content exclusions](../06-privacy-safeguards/privacy-settings.md) for sensitive files
- Understand that for GitHub Copilot Free/Individual, prompts may be used for model improvement (unless opted out)
- Use Copilot for Business/Enterprise, which excludes prompts from training by default

---

### 3. Intellectual Property Harms
Copilot may suggest code that closely resembles publicly available code with restrictive licenses:
- GPL, LGPL, AGPL code could impose copyleft obligations
- MIT or Apache-licensed code typically has fewer restrictions but still requires attribution in some contexts
- Proprietary code suggestions could constitute infringement

**Mitigation Strategies:**
- Enable the "Suggestions matching public code" duplication filter
- Review any substantial code block (>5 lines) for license implications
- Consult legal counsel for high-risk or commercial projects

---

### 4. Bias and Discrimination Harms
Bias in training data can produce outputs that:
- Reinforce stereotypes in code comments or documentation
- Implement algorithmic discrimination (e.g., biased scoring functions)
- Overlook accessibility requirements

**Mitigation Strategies:**
- Apply inclusive language standards in code reviews
- Test algorithmic suggestions for fairness where human impact is involved
- Supplement Copilot with explicit diversity and inclusion guidelines in prompts

---

### 5. Quality and Reliability Harms
Accepting unverified AI suggestions can degrade software quality:
- Subtle logic errors that pass testing but fail in production
- Hallucinated function calls to non-existent APIs
- Incomplete error handling

**Mitigation Strategies:**
- Treat AI suggestions as an initial draft, not final code
- Write unit tests before accepting suggestions (test-driven workflow)
- Perform human peer code review

---

### 6. Over-Reliance and Skill Atrophy
Long-term harms include:
- Reduced developer problem-solving ability
- Teams becoming dependent on Copilot for basic tasks
- Loss of critical thinking in code review

**Mitigation Strategies:**
- Use Copilot as a productivity booster, not a substitute for learning
- Periodically work without Copilot to maintain core skills
- Encourage understanding of accepted suggestions, not just copy-paste

---

## Harm vs. Mitigation Summary Table

| Harm Category | Example | Mitigation |
|---|---|---|
| Security | SQL injection in generated query | CodeQL scanning, security review |
| Privacy | PII in prompt | Content exclusions, no raw data in prompts |
| IP | GPL code reproduced | Public code filter, legal review |
| Bias | Stereotyped variable names | Inclusive review standards |
| Quality | Hallucinated API | Testing, peer review |
| Over-reliance | Accepting without understanding | Deliberate learning practice |

---

## Key Takeaways

- Harm from AI tools is often unintentional but real.
- Mitigation is a layered approach: tool configuration + code review + testing + education.
- Organizations should establish policies that address each category of harm.
- Individuals remain responsible for the code they accept and deploy.

---

[← Back to Responsible AI](README.md)
