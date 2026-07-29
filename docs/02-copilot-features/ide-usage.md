# Using GitHub Copilot in the IDE

GitHub Copilot integrates directly into popular IDEs to provide real-time coding assistance.

---

## Enabling Copilot in the IDE

### Prerequisites
1. An active GitHub Copilot subscription (Individual, Business, or Enterprise)
2. A supported IDE (VS Code, Visual Studio, JetBrains IDEs, Neovim, Xcode)
3. The GitHub Copilot extension installed

### Steps to Enable in VS Code
1. Open VS Code
2. Go to the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for "GitHub Copilot"
4. Click **Install** on the "GitHub Copilot" extension (and optionally "GitHub Copilot Chat")
5. Sign in with your GitHub account when prompted
6. Confirm your account has an active Copilot subscription
7. The Copilot icon in the status bar confirms activation

### Enabling/Disabling Copilot
- **Globally**: Click the Copilot icon in the status bar and toggle on/off
- **Per language**: `GitHub Copilot: Enable/Disable for [language]` in the command palette
- **Via settings**: `"github.copilot.enable": { "*": true, "plaintext": false }`

---

## Triggering Copilot Through Inline Suggestions

Copilot provides suggestions automatically as you type.

### How It Works
1. Start typing code or a comment
2. Copilot analyzes the context and generates a suggestion (shown in gray "ghost text")
3. Press `Tab` to accept the full suggestion
4. Press `Escape` to dismiss
5. Use `Alt+]` / `Option+]` to cycle to the next suggestion
6. Use `Alt+[` / `Option+[` to cycle to the previous suggestion

### Partial Acceptance (VS Code)
- `Ctrl+Right` / `Cmd+Right`: Accept the next word only
- Useful when you want part of a suggestion but not all of it

### Best Practices for Inline Suggestions
- Write descriptive comments before the code you want generated
- Use function/method names that clearly indicate intent
- Break complex tasks into smaller, individually suggestable pieces

---

## Triggering Copilot Through Chat

Copilot Chat provides a conversational interface for more complex interactions.

### Opening Copilot Chat
- **VS Code**: Click the chat icon in the sidebar, or press `Ctrl+Alt+I` / `Cmd+Alt+I`
- **Inline chat**: Select code and press `Ctrl+I` / `Cmd+I` for an inline chat box

### Chat Slash Commands
| Command | Description |
|---|---|
| `/explain` | Explain how selected code works |
| `/fix` | Suggest a fix for a problem in the selected code |
| `/tests` | Generate unit tests for the selected code |
| `/doc` | Generate documentation for the selected code |
| `/optimize` | Suggest performance improvements |
| `/new` | Scaffold a new project or file |
| `/clear` | Clear the chat history |

### Chat Participants (Scoping Context)
- `@workspace`: Include workspace context in the conversation
- `@vscode`: Questions about VS Code itself
- `@terminal`: Questions related to the terminal

### Context Variables
- `#file`: Reference a specific file
- `#selection`: Reference the current selection
- `#editor`: Reference the current editor contents
- `#codebase`: Search across the full codebase

---

## Triggering Copilot in Agent Mode

Agent Mode allows Copilot to perform multi-step tasks autonomously. See [Advanced Features](advanced-features.md) for details.

---

## Configuring Content Exclusions

Content exclusions prevent Copilot from using specific files or repositories as context for suggestions.

### Purpose
- Protect sensitive files (e.g., `.env`, config files with secrets)
- Exclude proprietary business logic from AI context
- Comply with legal or regulatory requirements

### How to Configure (Repository Level)
1. Go to your repository on GitHub
2. Navigate to **Settings → Copilot**
3. Under **Content exclusion**, specify file paths or glob patterns

### How to Configure (Organization Level)
1. Go to your organization on GitHub
2. Navigate to **Settings → Copilot → Content exclusion**
3. Define patterns that apply across all repositories

### Example Patterns
```
# Exclude all .env files
**/.env

# Exclude a specific directory
/internal/secrets/**

# Exclude a file type across the repo
**/*.key
```

### IDE Behavior with Exclusions
- Excluded files are shown with a Copilot icon with a slash in the status bar
- Copilot will not provide suggestions while an excluded file is active in the editor
- Copilot will not use excluded files as context for suggestions in other files

---

## Key Takeaways

- Copilot integrates into the IDE via an extension and provides inline suggestions, Chat, and Agent Mode.
- Inline suggestions are accepted with `Tab` and dismissed with `Escape`.
- Chat slash commands (`/explain`, `/fix`, `/tests`, etc.) provide structured interactions.
- Content exclusions protect sensitive files from being used as AI context.

---

[← Back to Features](README.md)
