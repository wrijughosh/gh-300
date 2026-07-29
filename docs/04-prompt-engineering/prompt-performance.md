# Engineering Prompts for Performance

Once you understand prompt crafting basics, prompt engineering focuses on optimizing prompts for consistent, high-quality, and efficient output.

---

## Prompt Engineering Principles

### Principle 1: Single Responsibility
Each prompt should have one clear objective. Avoid asking for multiple unrelated things in a single prompt.

❌ "Write a login function, a registration function, and also generate some sample user data and unit tests"

✅ Send four separate, focused prompts:
1. "Write a login function..."
2. "Write a registration function..."
3. "Generate sample user data..."
4. "Write unit tests for the login function..."

### Principle 2: Iterative Refinement
Start with a basic prompt, review the output, and refine through follow-up prompts.

```
Turn 1: "Write a cache class for storing API responses"
[Review output]
Turn 2: "Add a TTL (time-to-live) parameter so entries expire after a configurable duration"
Turn 3: "Make it thread-safe using a lock"
Turn 4: "Add a method to invalidate all entries matching a given prefix"
```

### Principle 3: Front-Load Important Context
Put the most critical information at the beginning of the prompt. LLMs give more weight to content earlier in the context window.

❌ "Write the database connection handler. It should work with PostgreSQL. Use psycopg2. Don't use ORM."

✅ "Using psycopg2 (no ORM), write a PostgreSQL connection handler that..."

### Principle 4: Explicit Over Implicit
State requirements explicitly rather than assuming Copilot will infer them from context.

❌ "Add error handling to this function" (what kind? for what errors?)

✅ "Add try/except blocks for database connection errors, invalid data format errors, and timeout errors. Log each error with the exception message, and re-raise connection errors as ApplicationException."

### Principle 5: Constraint-First for Security
State security requirements upfront rather than as an afterthought.

✅ "Write a file upload handler. Requirements: only accept .jpg, .png, .pdf; maximum 5MB; validate MIME type not just extension; store files in /uploads/{uuid} to prevent path traversal; return only the file ID, never the path."

---

## Prompt Process Flow

Understanding the flow helps you predict how Copilot will respond:

```
1. Collect context (files, cursor, chat history)
2. Apply system prompt (language, model behavior)
3. Assemble user prompt (your message + context)
4. Truncate to context window
5. Send to model
6. Model generates completion token-by-token
7. Apply filters
8. Return to developer
```

**Implication**: If your prompt contains a lot of context, earlier content may be truncated. For Chat, this means very long conversations may lose context from earlier turns.

---

## Chat History Usage

### How Copilot Uses Chat History
- Each message in a Copilot Chat session is part of the conversation context
- Copilot references prior turns to maintain coherence
- Corrections and refinements in prior turns inform subsequent responses

### Managing Chat History Effectively
- **Start a new chat** when switching to a completely different topic
- **Summarize** complex prior context at the start of a follow-up session
- **Reference specific turns** when asking for modifications: "In the previous function you wrote..."
- Use `/clear` to reset the conversation when starting fresh

### Chat History Limits
- Very long conversations consume the context window
- When the limit is reached, the oldest messages are dropped
- This can cause Copilot to "forget" early context
- Strategy: periodically recap key decisions in a follow-up message

---

## Prompt File Reuse

### What Are Prompt Files?
Prompt files are `.prompt.md` files saved in your workspace that contain reusable prompt templates.

### Creating a Prompt File
Create a file like `.github/prompts/api-endpoint.prompt.md`:
```markdown
---
mode: chat
---
Create a REST API endpoint following our conventions:
- Use our custom `@router.get/post/put/delete` decorators from `app/routing.py`
- All responses must use the `ApiResponse` wrapper class
- Include input validation using Pydantic models
- Add OpenAPI docstrings with examples
- Write unit tests using pytest and our `MockDatabase` fixture

Endpoint specification:
{{ENDPOINT_SPEC}}
```

### Using Prompt Files
- Reference with `#file:.github/prompts/api-endpoint.prompt.md` in Chat
- Prompt files ensure consistency across the team
- Reduces prompt repetition for common tasks
- Can be shared via version control

---

## Advanced Prompting Techniques

### Chain-of-Thought Prompting
Ask Copilot to reason through a problem step by step before producing code:
```
"Think through the edge cases for a binary search implementation in Python, 
then write the implementation that handles all of them."
```

### Role Prompting
Assign Copilot a specific expert persona:
```
"As a security engineer reviewing this authentication code, identify any 
vulnerabilities and suggest fixes."
```
```
"As a performance engineer, analyze this database query and suggest 
optimizations for a table with 50 million rows."
```

### Negative Constraints
Explicitly state what you do NOT want:
```
"Write a sorting function. Do NOT use Python's built-in sort() or sorted(). 
Do NOT use any libraries. Implement quicksort from scratch."
```

### Template Filling
Use templates in your codebase as examples:
```
"Following the same pattern as the `getUserById` function in this file, 
implement `getOrdersByUserId`"
```

---

## Common Prompt Anti-Patterns

| Anti-Pattern | Problem | Better Approach |
|---|---|---|
| Vague task | "Fix this" | Describe the specific issue |
| No constraints | "Write a login function" | Specify language, framework, security requirements |
| Multiple goals | "Do X, Y, and Z" | One prompt per goal |
| Ignoring output | Accept without reading | Review before accepting |
| Long unfocused context | Paste entire codebase | Provide only relevant files/snippets |
| No examples for novel format | Expect format from nothing | Use few-shot with 1–2 examples |

---

## Key Takeaways

- Prompt engineering principles: single responsibility, iterative refinement, front-load context, explicit constraints, security-first.
- Chat history is used for coherence but has limits—start new chats for unrelated topics.
- Prompt files enable reusable, consistent prompts that can be versioned and shared.
- Advanced techniques like chain-of-thought, role prompting, and negative constraints produce more reliable output.

---

[← Back to Prompt Engineering](README.md)
