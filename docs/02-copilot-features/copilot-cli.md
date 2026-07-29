# Using GitHub Copilot CLI

GitHub Copilot CLI brings AI assistance directly to the command line, helping developers work with shell commands, scripts, and the terminal more efficiently.

---

## What is GitHub Copilot CLI?

GitHub Copilot CLI is an extension for the GitHub CLI (`gh`) that provides AI-powered assistance in the terminal. It helps developers:
- Explain unfamiliar commands
- Suggest commands for described tasks
- Generate and refine shell scripts
- Work interactively to build complex pipelines

**Key benefit**: Developers no longer need to leave the terminal to search for command syntax, flags, or shell patterns.

---

## Installing GitHub Copilot CLI

### Prerequisites
- GitHub CLI (`gh`) version 2.x or later
- An active GitHub Copilot subscription (Individual, Business, or Enterprise)

### Installation Steps

1. **Install the GitHub CLI** (if not already installed):
   ```bash
   # macOS
   brew install gh
   
   # Windows
   winget install --id GitHub.cli
   
   # Linux (Debian/Ubuntu)
   sudo apt install gh
   ```

2. **Authenticate with GitHub**:
   ```bash
   gh auth login
   ```

3. **Install the Copilot CLI extension**:
   ```bash
   gh extension install github/gh-copilot
   ```

4. **Verify the installation**:
   ```bash
   gh copilot --version
   ```

### Updating Copilot CLI
```bash
gh extension upgrade gh-copilot
```

---

## Key GitHub Copilot CLI Features and Commands

### `gh copilot suggest`
Suggests a shell command for a natural-language description.

```bash
gh copilot suggest "list all running Docker containers sorted by memory usage"
```

**Output**: Copilot returns a suggested command and offers to:
- Copy the command to the clipboard
- Execute the command directly
- Revise the suggestion with follow-up input

### `gh copilot explain`
Explains what a shell command does.

```bash
gh copilot explain "find . -name '*.log' -mtime +7 -delete"
```

**Output**: A plain-language explanation of each part of the command.

### Command Type Flags
Both `suggest` and `explain` accept a `-t` or `--target` flag to specify the type of command:
- `gh` — GitHub CLI commands
- `shell` — general shell commands (default)
- `git` — Git commands

```bash
gh copilot suggest -t git "undo the last commit but keep the changes staged"
```

---

## Using GitHub Copilot CLI Interactively and in Sessions

### Interactive Mode
After running `suggest`, Copilot enters an interactive loop where you can:
- **Execute**: Run the suggested command immediately
- **Copy to clipboard**: Paste the command elsewhere
- **Revise**: Provide additional context to refine the suggestion
- **Cancel**: Exit without executing

### Example Interactive Session
```
$ gh copilot suggest "compress a directory excluding node_modules"

Suggestion:
  tar --exclude='./node_modules' -czf archive.tar.gz ./my-project

? What would you like to do?
  ❯ Execute command
    Copy command to clipboard
    Revise command
    Cancel
```

### Session Continuity
- Each `gh copilot suggest` or `gh copilot explain` invocation is a new session
- Context is not automatically retained between commands
- For related commands, provide context in each invocation or use `revise` within the same session

---

## Generating Scripts and Managing Files with GitHub Copilot CLI

### Generating Scripts
Copilot CLI can help generate entire shell scripts through iteration:

```bash
# Start with a high-level description
gh copilot suggest "bash script to back up all MySQL databases to S3"
```

**Workflow**:
1. Generate an initial suggestion
2. Use **Revise** to add error handling, logging, or specific requirements
3. Copy the refined script to a file
4. Review and test before executing

### Managing Files
Common file management tasks Copilot CLI excels at:
- Bulk rename operations
- Finding and deleting files by pattern
- Archiving and compressing directories
- Transforming file contents with `awk`, `sed`, or `jq`

```bash
gh copilot suggest "recursively find all .DS_Store files and delete them"
gh copilot explain "awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -20"
```

---

## Key Takeaways

- Copilot CLI is installed as a `gh` extension: `gh extension install github/gh-copilot`
- The two primary commands are `gh copilot suggest` and `gh copilot explain`
- Interactive sessions allow iterative refinement without re-typing the full prompt
- Copilot CLI reduces context-switching between terminal and browser for command lookups

---

[← Back to Features](README.md)
