# Crafting Effective Prompts

A well-crafted prompt is the most important factor in getting high-quality suggestions from GitHub Copilot.

---

## Prompt Structure and Context

### What Makes a Good Prompt?

A good prompt for Copilot contains:

1. **Goal**: What you want Copilot to do
2. **Context**: Relevant background information (language, framework, constraints)
3. **Format**: How you want the output structured
4. **Examples** (when appropriate): Samples of expected input/output

### Prompt Anatomy

```
[Role/Context] + [Task description] + [Constraints/Requirements] + [Examples (optional)]
```

**Example – Weak Prompt**:
```
// function to process data
```

**Example – Strong Prompt**:
```
// Python function that takes a list of user dictionaries (each with 'name', 'email', 'age'),
// validates that each email is a valid format and each age is between 18-120,
// and returns a tuple of (valid_users, invalid_users).
// Uses only standard library modules. Include type hints.
```

---

## Understanding How Context Is Determined

Copilot automatically assembles context from multiple sources, ranked by relevance:

### Automatic Context Sources (in order of priority)
1. **Current file**: Code immediately before and after the cursor
2. **Open editor tabs**: Files currently open in the editor
3. **Recently opened files**: Files opened in the current session
4. **Related files**: Files with matching imports or references
5. **Chat history**: Prior messages in the current conversation

### How to Guide Context
Since context is automatic, developers can guide it by:
- **Opening relevant files** before asking a question
- **Writing descriptive comments** above the code area
- **Using chat references** (`#file`, `#selection`, `#codebase`)
- **Starting prompts with background**: "Given the User model defined in `models/user.py`..."

---

## Zero-Shot and Few-Shot Prompting

### Zero-Shot Prompting
Ask Copilot to perform a task without providing any examples.

**Works best when**:
- The task is common and well-understood
- Copilot has strong training data for the task type
- The task is simple or follows a clear pattern

**Example**:
```
// Write a function to calculate the Fibonacci sequence up to n
```

### Few-Shot Prompting
Provide one or more examples of the desired input/output before asking for the target output.

**Works best when**:
- The task has a specific format or style
- The pattern is not common in training data
- Consistent output structure is important

**Example**:
```javascript
// Transform user objects to a display format:
// Input: { first_name: "Jane", last_name: "Doe", created_at: "2023-01-15" }
// Output: { displayName: "Jane Doe", memberSince: "January 2023" }

// Input: { first_name: "John", last_name: "Smith", created_at: "2022-07-04" }
// Output: { displayName: "John Smith", memberSince: "July 2022" }

// Now transform:
// Input: { first_name: "Alice", last_name: "Johnson", created_at: "2024-03-20" }
function transformUser(user) {
```

---

## Best Practices for Prompt Crafting

### Be Specific
❌ `// function to sort data`  
✅ `// Sort a list of Employee objects by (department ascending, salary descending). Python 3.10+`

### Specify Constraints
- Language version: "Python 3.11", "ES2020"
- Libraries to use or avoid: "use only stdlib", "use lodash for utility functions"
- Performance requirements: "must run in O(n log n) or better"
- Error handling: "raise ValueError for invalid input", "return None on failure"

### Use the Right Abstraction Level
- For functions: describe inputs, outputs, and side effects
- For classes: describe responsibilities and key behaviors
- For tests: describe the scenario and expected behavior

### Provide File-Level Context
Start files with a header comment describing the module's purpose:
```python
# authentication/jwt_handler.py
# Handles JWT token creation, validation, and refresh logic.
# Uses PyJWT library. Tokens expire after 24 hours.
# Do not use datetime.utcnow() - use timezone-aware timestamps.
```

### Use Chat for Complex Tasks
For multi-step or complex requirements, use Chat instead of inline comments:
```
Create a TypeScript class for managing a connection pool to PostgreSQL.
Requirements:
- Maximum 10 connections
- Idle connections time out after 30 seconds
- Queue requests when pool is exhausted (up to 100 queued requests)
- Expose connect(), release(), and drain() methods
- Include JSDoc comments
```

---

## Key Takeaways

- Good prompts have a clear goal, relevant context, explicit constraints, and optionally examples.
- Context is automatically assembled from open files and chat history—guide it by opening relevant files and writing descriptive comments.
- Zero-shot prompting works for common tasks; few-shot prompting is better for novel patterns or specific formats.
- Specificity is the most impactful single improvement you can make to a prompt.

---

[← Back to Prompt Engineering](README.md)
