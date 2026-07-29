# Domain 3: Understand GitHub Copilot Data and Architecture (10–15%)

This domain covers how GitHub Copilot handles data, processes prompts, and manages the lifecycle of a code suggestion.

---

## Exam Objectives

- [Data Handling and Flow](data-handling-flow.md)
- [Lifecycle and Limitations](lifecycle-limitations.md)

---

## Key Themes

1. **Privacy by design**: Copilot Business and Enterprise plans have data usage defaults that protect organizational code.
2. **Prompt building is automatic**: Copilot assembles context from multiple sources to construct effective prompts.
3. **Filtering happens at multiple stages**: Both before the prompt is sent and after the response is received.
4. **LLMs have fundamental limitations**: Understanding these prevents misplaced trust in Copilot's output.

---

## Architecture Overview

```
Developer types code
        ↓
Copilot extension collects context
(open files, cursor position, adjacent code)
        ↓
Prompt is assembled (pre-processing)
        ↓
Prompt sent to Copilot proxy (GitHub)
        ↓
Proxy applies content filtering
        ↓
Request forwarded to LLM (OpenAI / Azure OpenAI)
        ↓
LLM generates completion
        ↓
Response returned to proxy
        ↓
Post-processing and filtering applied
        ↓
Suggestion displayed in IDE
        ↓
Developer accepts or rejects
```

---

[← Back to Study Guide](../../README.md) | [Next: Prompt Engineering →](../04-prompt-engineering/README.md)
