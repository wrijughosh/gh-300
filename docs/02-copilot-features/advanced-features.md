# Advanced Features: Agent Mode, Copilot Edits, MCP, Spaces, Spark, and More

This section covers the extended capabilities of GitHub Copilot beyond basic inline suggestions, including autonomous task execution, multi-file editing, and platform-level features.

---

## Agent Mode

### What is Agent Mode?
Agent Mode enables Copilot to autonomously perform multi-step coding tasks. Instead of providing a single suggestion, Copilot can:
- Plan and execute a sequence of coding steps
- Read, create, and edit multiple files
- Run terminal commands (with user confirmation)
- Iterate based on error messages or test results

### How to Enable Agent Mode
1. Open Copilot Chat in VS Code
2. Switch the chat mode dropdown from **Ask** to **Agent**
3. Enter a high-level task description

### Example Use Case
```
Agent: "Create a REST API endpoint that returns paginated user records from a PostgreSQL database, including unit tests"
```
Copilot will:
1. Identify existing database models and connection setup
2. Create the endpoint in the appropriate route file
3. Add necessary query logic
4. Generate unit tests
5. Update imports and dependencies as needed

### Agent Sessions
- Each Agent Mode conversation is an **Agent Session**
- Sessions maintain context across multiple tool calls and file edits within the conversation
- Sessions can be paused and resumed
- For large or complex tasks, **Sub-Agents** can be delegated specific sub-tasks

### Sub-Agents
Sub-Agents allow the primary agent to delegate specific tasks to specialized agents:
- **Optimizes context usage** by keeping each agent's context window focused
- Useful for long-running tasks with distinct phases (e.g., backend agent + frontend agent)
- Sub-agent results are synthesized by the primary agent

### Best Practices for Agent Mode
- Start with a clear, specific description of the desired outcome
- Define the scope explicitly (e.g., "only modify files in the `src/api` directory")
- Review each file change before confirming
- Use `YOLO mode` (auto-approve) only in isolated environments

---

## Copilot Edits

### What is Copilot Edits?
Copilot Edits is a feature for targeted, multi-file code refactoring from a single instruction.

### How to Use Copilot Edits
1. Select the files you want to include in scope
2. Open Copilot Chat and switch to **Edit** mode
3. Describe the change: "Rename all occurrences of `userId` to `accountId` across these files"
4. Review the proposed diff and apply or reject changes file by file

### Copilot Edits vs. Agent Mode
| Feature | Copilot Edits | Agent Mode |
|---|---|---|
| Scope | Specific files, targeted changes | Broader, multi-step tasks |
| Autonomy | Lower (you scope the files) | Higher (agent discovers files) |
| Best for | Refactoring, renaming, formatting | Building features, fixing bugs end-to-end |

---

## Model Context Protocol (MCP)

### What is MCP?
The **Model Context Protocol** is an open standard that allows Copilot to integrate with external tools and data sources, extending its capabilities beyond the local codebase.

### How MCP Works
- MCP servers expose tools (functions) that Copilot can call during agentic workflows
- Tools can include: database queries, API calls, file system access, search engines, and more
- Copilot uses MCP tools autonomously when they are relevant to the current task

### Setting Up MCP in VS Code
1. Install the MCP server for your tool (e.g., a GitHub MCP server, a database MCP server)
2. Configure the MCP server in your VS Code settings:
   ```json
   {
     "github.copilot.mcpServers": {
       "my-db-server": {
         "command": "node",
         "args": ["/path/to/mcp-server.js"]
       }
     }
   }
   ```
3. The MCP server's tools become available to Copilot in Agent Mode

### Use Cases for MCP
- Querying a live database to inform code generation
- Fetching documentation from an internal wiki
- Interacting with issue trackers or project management tools
- Running custom validation or analysis scripts

---

## GitHub Copilot for Code Review

### Copilot Code Review
- Available in GitHub Pull Requests on github.com
- Copilot reviews changed files and posts inline comments
- Identifies potential bugs, anti-patterns, and style issues
- Organization admins can enable Copilot Code Review as a required reviewer

### Review Instructions Files
Organizations can customize Copilot's review behavior with instructions files:
- File location: `.github/copilot-instructions.md` or `.github/copilot-review-instructions.md`
- Contents define coding standards, review priorities, and project-specific patterns

---

## Spaces and Spark

### GitHub Copilot Spaces
- **Spaces** are collaborative AI workspaces on github.com
- Allow teams to work with Copilot in a shared context
- Useful for knowledge sharing and collaborative problem-solving

### GitHub Spark
- **Spark** is a feature that generates full web applications from a natural-language description
- No code writing required—Spark scaffolds the entire application
- Useful for rapid prototyping, internal tools, and demos

---

## Pull Request Summaries

### What Are PR Summaries?
Copilot can automatically generate a summary of a pull request based on the changes:
- Describes what was changed and why
- Lists files affected
- Highlights potential areas of concern

### How to Use
1. Create or open a pull request on github.com
2. Click **Copilot** → **Summarize** in the PR description area
3. Review and edit the generated summary before saving

---

## Copilot Chat Limits, Options, Feedback, and Commands

### Limits
- Chat messages have a maximum length
- The context window limits how much code can be included in a single conversation
- Extended conversations may lose early context; start a new chat for new topics

### Feedback
- Thumbs up/down buttons on each response provide feedback to GitHub
- Use `/feedback` in chat to report specific issues

### Prompt File Reuse
- Save frequently used prompts as `.prompt.md` files in your workspace
- Reuse them in Chat with the `#file` reference or via the prompt picker
- Ensures consistent instructions across sessions and team members

---

## Key Takeaways

- Agent Mode enables multi-step autonomous coding with Sub-Agent delegation for optimized context
- Copilot Edits targets specific file sets for focused refactoring
- MCP extends Copilot with external tool integrations
- Spaces and Spark enable collaborative and rapid-prototyping workflows on github.com
- PR Summaries automate pull request documentation
- Prompt files enable reusable, consistent prompting patterns

---

[← Back to Features](README.md)
