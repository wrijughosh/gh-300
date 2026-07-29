# Validating AI Output

Validation is a non-negotiable step in responsible AI usage. GitHub Copilot suggestions must be verified before they are accepted, committed, and deployed.

---

## Why Validation Matters

AI models generate output based on statistical patterns—they do not "know" whether their suggestions are correct. Without validation:
- Bugs are introduced silently
- Security vulnerabilities are shipped to production
- Technical debt accumulates from misunderstood code
- Legal risks increase from unvetted licensing

---

## What Needs to Be Validated

### Correctness
Does the code do what it is supposed to do?
- Run the code and observe the output
- Write unit tests that cover the expected behavior
- Use integration tests to validate interactions with external systems

### Security
Is the code free of common vulnerabilities?
- Review for OWASP Top 10 issues (injection, broken auth, XSS, etc.)
- Run static analysis tools (e.g., CodeQL, Semgrep)
- Run secret scanning to detect hard-coded credentials

### Performance
Is the code efficient enough for its context?
- Review time and space complexity for data-intensive operations
- Profile if performance is critical

### Readability and Maintainability
Can other developers understand and maintain the code?
- Ensure naming conventions are consistent
- Check that logic is clear, not just functional

### License Compliance
Does the code comply with licensing requirements?
- Check if suggestions match known open-source code
- Use the public code matching filter

---

## Validation Techniques

### 1. Manual Code Review
The most fundamental validation technique:
- Read through every line of accepted suggestion
- Understand the logic before committing
- Apply your team's code review checklist

### 2. Automated Testing
- **Unit tests**: Validate individual functions and methods
- **Integration tests**: Validate interactions between components
- **End-to-end tests**: Validate complete user workflows

### 3. Static Analysis
- **CodeQL**: GitHub's semantic code analysis engine
- **Dependabot**: Scans dependencies for known vulnerabilities
- **Secret scanning**: Detects accidentally committed secrets

### 4. Dynamic Testing
- Run the application and test the suggestion in context
- Use fuzz testing for security-critical code paths

### 5. Peer Review
- Have a teammate review AI-generated code sections
- Treat AI suggestions with the same rigor as any other PR contribution

---

## Validation Workflow (Recommended)

```
1. Receive Copilot suggestion
2. Read and understand the suggestion
3. Does it make sense for the context? → If no, dismiss and rephrase prompt
4. Accept suggestion
5. Write or update unit tests
6. Run static analysis
7. Commit only after all checks pass
8. Include AI-generated sections in code review
```

---

## When to Reject a Suggestion

Reject a Copilot suggestion when:
- You don't understand what it does
- It references functions or modules that don't exist
- It introduces obvious security risks (hard-coded secrets, unsafe eval, etc.)
- It significantly deviates from your codebase's conventions
- Testing fails and the cause is in the generated code

---

## Key Takeaways

- Validation is required for every AI suggestion—no exceptions.
- Validation combines manual review, automated testing, and static analysis.
- Accepting suggestions without validation is the primary source of AI-introduced bugs.
- A good prompt reduces the need for validation by reducing the likelihood of poor output, but never eliminates it.

---

[← Back to Responsible AI](README.md)
