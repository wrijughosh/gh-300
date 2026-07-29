# Data Handling and Flow

Understanding how GitHub Copilot processes and handles your data is essential for making informed decisions about privacy and compliance.

---

## Data Usage, Flow, and Sharing

### What Data Does Copilot Use?

When you use GitHub Copilot in the IDE, the following data is involved:

| Data Type | Description |
|---|---|
| **Prompts** | Code context sent to the model, including the content of open files and cursor context |
| **Completions** | The code suggestions returned by the model |
| **Usage telemetry** | Metadata about suggestion acceptance rates, latency, and errors |
| **User engagement data** | How users interact with suggestions (accepted, dismissed, modified) |

### Data Transmission Flow

1. **Local collection**: The Copilot IDE extension collects context from your editor
2. **HTTPS transmission**: Data is sent over an encrypted connection to GitHub's Copilot proxy
3. **Proxy processing**: GitHub's proxy applies filters and forwards to the AI model
4. **Model inference**: The AI model generates a completion
5. **Return**: The completion travels back through the proxy to your IDE

### Who Receives the Data?

- **GitHub**: Receives all prompts and completions via the proxy
- **OpenAI / Azure OpenAI**: Receives prompts and generates completions
- **Third parties**: Data is not sold to or shared with third parties for advertising

---

## Data Usage by Plan

| Plan | Prompts used for training? | Default |
|---|---|---|
| GitHub Copilot Individual | Yes, unless opted out | Training ON |
| GitHub Copilot Business | No | Training OFF |
| GitHub Copilot Enterprise | No | Training OFF |

### How to Opt Out (Individual Plan)
1. Go to **GitHub.com → Settings → Copilot**
2. Under **Suggestions**, uncheck "Allow GitHub to use my code snippets for product improvements"

---

## Input Processing and Prompt Building

### What Goes Into a Prompt?

Copilot builds prompts automatically using context from multiple sources:

1. **Current file content**: The code before and after the cursor
2. **Open tabs**: Content from other files currently open in the editor
3. **Related files**: Files that are semantically related (imports, related modules)
4. **Comments and docstrings**: Natural language instructions near the cursor
5. **Chat history**: Previous messages in the current Copilot Chat session
6. **Repository context**: For Copilot Enterprise, repository-wide index is available

### Prompt Construction Process

```
Context Sources → Ranking/Relevance Scoring → Truncation to fit context window → Prompt Assembly → Send
```

- Copilot uses a **ranking algorithm** to select the most relevant context
- Content is prioritized by proximity to the cursor and semantic relevance
- The final prompt is truncated to fit within the model's **context window** limit

### Context Window
- The context window is the maximum amount of text (measured in tokens) the model can process at once
- Tokens are roughly equivalent to words or word fragments
- Larger files or longer Chat conversations consume more of the context window
- When the context window is exceeded, older content is dropped

---

## Proxy Filtering and Post-Processing

### Pre-Request Filtering (Prompt Filtering)
Before sending the prompt to the LLM, the proxy checks for:
- **Personally Identifiable Information (PII)**: Detected patterns (e.g., SSNs, email addresses) may be flagged
- **Toxic content**: Requests that might generate harmful output are blocked
- **Policy violations**: Content that violates GitHub's Terms of Service

### Post-Response Filtering (Completion Filtering)
After the LLM generates a completion, the proxy applies:

1. **Profanity and offensive content filter**: Removes or blocks offensive suggestions
2. **Duplication detection / public code matching filter**: Detects completions that closely match publicly available code (≥150 characters matching a known source)
   - If enabled (block), such completions are withheld
   - If disabled (allow), completions are shown with a warning
3. **Security vulnerability filtering**: Patterns matching known vulnerability signatures may be blocked

### How Filtering Is Configured
- Organization admins configure these settings in **Organization Settings → Copilot → Policies**
- The "Suggestions matching public code" setting is either **Allowed** or **Blocked**
- Individual users can configure this in their personal Copilot settings (if not overridden by org policy)

---

## Data Retention

| Data Type | Retention Period |
|---|---|
| Prompts and completions | Discarded after short period (not stored long-term for Business/Enterprise) |
| Telemetry data | Retained per GitHub's privacy policy |
| Chat session data | Retained for the duration of the session; not persisted |

---

## Key Takeaways

- Copilot collects code context (prompts) from the IDE, transmits it to GitHub's proxy, and routes it to an AI model.
- Business and Enterprise plans do not use prompts for model training by default.
- Prompts are assembled from multiple context sources and trimmed to fit the model's context window.
- Filtering occurs both before the prompt is sent (toxic content, PII) and after the completion is received (public code matching, offensive content).

---

[← Back to Data and Architecture](README.md)
