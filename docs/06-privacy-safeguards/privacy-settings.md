# Managing Privacy Settings and Content Exclusions

GitHub Copilot provides multiple layers of privacy control to protect sensitive code, comply with regulations, and meet organizational requirements.

---

## Configuring Content Exclusions

Content exclusions tell Copilot to ignore specific files or directories when generating suggestions. Excluded content is not used as context and Copilot will not make suggestions when an excluded file is the active editor.

### Why Use Content Exclusions?

- **Security**: Exclude files containing secrets (`.env`, credentials files, key files)
- **Privacy**: Exclude files containing PII or sensitive business data
- **Legal/Compliance**: Exclude files covered by strict IP protections
- **License protection**: Exclude code that carries restrictive licensing conditions

### Configuring at the Repository Level

1. Navigate to the repository on GitHub
2. Go to **Settings → Copilot**
3. Under **Content exclusion**, add glob patterns

**Example patterns**:
```
# Exclude environment files
**/.env
**/.env.*
**/secrets.yaml
**/credentials.json

# Exclude private business logic
/src/pricing/internal/**
/src/algorithms/proprietary/**

# Exclude key and certificate files
**/*.pem
**/*.key
**/*.p12

# Exclude a specific directory
/confidential/**
```

### Configuring at the Organization Level

Organization admins can define exclusions that apply across all repositories:

1. Go to **Organization Settings → Copilot → Content exclusion**
2. Add patterns (same glob syntax as repository-level)
3. These patterns are merged with any repository-level exclusions

**When organization and repository exclusions conflict**: The most restrictive setting wins—content excluded at either level is excluded everywhere.

### How IDE Behavior Changes with Exclusions

| Scenario | Behavior |
|---|---|
| Excluded file is the active editor | No suggestions are shown; Copilot icon shows a slash |
| Excluded file is open in another tab | That file is not used as context |
| Cursor is in a non-excluded file | Normal suggestions, but excluded files are not used as context |

---

## Configuring Editor Settings

### VS Code Settings for Privacy
In VS Code's `settings.json`:

```json
{
  // Disable Copilot for specific languages globally
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": false,
    "yaml": true
  },
  
  // Enable/disable inline suggestions
  "editor.inlineSuggest.enabled": true
}
```

### Per-Workspace Settings
Create `.vscode/settings.json` in your workspace to apply settings only to that project:
```json
{
  "github.copilot.enable": {
    "*": true,
    "dotenv": false
  }
}
```

---

## Ownership and Limitations of Outputs

### Who Owns Copilot-Generated Code?

This is a legally nuanced area. Key points:

1. **GitHub's Terms of Service**: GitHub states that you own the output Copilot generates when you use it.
2. **No copyright for pure AI generation**: In many jurisdictions (including the US), purely AI-generated content without meaningful human authorship may not be copyrightable.
3. **Human + AI collaboration**: When a developer meaningfully contributes to, modifies, and integrates AI-generated code, the human contribution may be copyrightable.
4. **Input code remains owned by the author**: Copilot's training on public code does not transfer ownership of that code to you.

### Limitations of Outputs

| Limitation | Description |
|---|---|
| Not always correct | Copilot can generate plausible but incorrect code |
| May reproduce public code | Suggestions can closely match existing open-source code |
| Not reviewed by legal experts | Copilot cannot provide legal advice |
| No warranty | GitHub provides no warranty for the correctness or legality of suggestions |

### Best Practices for Ownership
- Document AI assistance in code reviews and commit messages
- Review all suggestions before committing to understand what you are accepting
- For commercially sensitive code, have legal counsel review AI-assisted output
- Enable the public code matching filter for projects with strict license requirements

---

## Understanding Plan-Level Privacy

### GitHub Copilot Individual
- Prompts and completions **may be used** to train/improve the model unless opted out
- **How to opt out**: GitHub Settings → Copilot → Suggestions → Uncheck "Allow GitHub to use my code snippets for product improvements"
- Feature access and privacy policies may change; check current GitHub documentation

### GitHub Copilot Business
- Prompts and completions are **not used** for model training by default
- No opt-in required
- Organization admins have full policy control
- Telemetry is still collected for usage analytics

### GitHub Copilot Enterprise
- Same as Business for data usage
- Additionally includes: repository indexing, custom knowledge bases, and enhanced context from the organization's codebase
- Highest level of enterprise policy controls

---

## Key Takeaways

- Content exclusions prevent sensitive files from being used as context and disable suggestions in excluded files.
- Configure exclusions at both repository and organization levels using glob patterns.
- Business and Enterprise plans do not use prompts for training by default; Individual plans do unless opted out.
- Ownership of AI-generated code is legally nuanced—developers should understand their organization's policies.
- Editor settings provide additional control over when and where Copilot suggestions are shown.

---

[← Back to Privacy and Safeguards](README.md)
