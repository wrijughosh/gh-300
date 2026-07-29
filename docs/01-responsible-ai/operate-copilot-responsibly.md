# Operating GitHub Copilot Responsibly

Operating Copilot responsibly means having an active, thoughtful approach to how you use, configure, and monitor the tool in your development workflow.

---

## Core Operational Principles

### 1. Know What Copilot Can and Cannot Do
Copilot is excellent at:
- Completing boilerplate and repetitive code
- Suggesting implementations from docstrings or comments
- Explaining unfamiliar code
- Generating tests from existing code
- Translating code between languages

Copilot should not be trusted without verification for:
- Security-critical code paths
- Complex business logic
- Novel algorithms
- Regulatory compliance requirements

### 2. Review Before You Accept
Never use "Accept All" for large blocks of generated code without reading them. Instead:
- Accept line by line when the block is complex
- Use partial acceptance to take only what you need
- Use the Chat panel to ask for explanations before accepting

### 3. Understand Organizational Policy
Organizations configure Copilot at multiple levels:
- **GitHub.com policies**: Enabled/disabled per organization, per repository
- **IDE settings**: Content exclusions by file path or pattern
- **Subscription tier**: Different privacy defaults (Individual vs. Business vs. Enterprise)

Always operate within the policies defined by your organization.

---

## Responsible Usage Practices

### Prompting
- Write clear, specific prompts with relevant context
- Avoid including sensitive data (PII, secrets, proprietary algorithms) in prompts
- Use comments and docstrings to guide suggestions

### Accepting Suggestions
- Read every suggestion before accepting
- Accept only suggestions you understand
- Test accepted suggestions immediately

### Reporting Issues
If Copilot generates harmful, offensive, or concerning output:
- Use the thumbs-down feedback button in the IDE
- Report via GitHub's feedback channels
- Document internally if required by your organization's AI incident process

### Tracking AI Usage
Some organizations require:
- Logging when AI assistance was used in significant code changes
- Including AI disclosure in PR descriptions
- Periodic reviews of AI-assisted code for quality metrics

---

## Responsible Configuration Checklist

| Setting | Recommended Action |
|---|---|
| Content exclusions | Configure for files containing secrets, PII, or proprietary logic |
| Public code matching | Enable to reduce license risk |
| Training data opt-out | Confirm your plan's default and opt out if required |
| Organization policies | Align your settings with your org's AI policy |
| Editor settings | Enable Copilot only in projects where it's permitted |

---

## Red Lines: What Copilot Should Never Be Used For

- Generating malware, ransomware, or exploit code
- Circumventing authentication or authorization systems
- Generating deceptive or manipulative content
- Automating attacks on systems or infrastructure
- Bypassing Copilot's own content filters

These uses violate GitHub's Terms of Service and may have legal consequences.

---

## Key Takeaways

- Responsible operation is an ongoing practice, not a one-time setup.
- Know your organization's policies and configure Copilot accordingly.
- Use feedback mechanisms to improve Copilot and protect other users.
- Never use Copilot for purposes that would violate GitHub's Terms of Service or your organization's policies.

---

[← Back to Responsible AI](README.md)
