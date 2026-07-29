# Organization-Wide Settings and Policies

GitHub Copilot provides extensive controls for organizations to manage how Copilot is used, what features are available, and how data is handled across the organization.

---

## Policy Management

### Accessing Organization Settings
1. Go to your organization on GitHub
2. Navigate to **Settings → Copilot**
3. Configure policies under the relevant sub-sections

### Feature Availability Controls
Organization admins can enable or disable specific Copilot features for their members:

| Feature | Control Level |
|---|---|
| GitHub Copilot (base) | Enable/disable for all, specific teams, or specific users |
| Copilot Chat (IDE) | Enable/disable organization-wide |
| Copilot Chat (github.com) | Enable/disable organization-wide |
| Copilot CLI | Enable/disable organization-wide |
| Copilot Code Review | Enable/disable, configure as required reviewer |
| Copilot in github.com | Enable/disable specific github.com features |
| Suggestions matching public code | Allow/Block |
| Training data opt-out | Opt out of using prompts/completions for training |

### Policy Enforcement
- Policies set at the organization level override user-level settings
- Enterprise admins can set policies that override organization-level settings
- Members cannot override organization-enforced policies

---

## Copilot Code Review Policies

### Enabling Copilot Code Review
1. Go to **Organization Settings → Copilot → Policies**
2. Enable **Copilot code review**
3. Optionally configure it as a **required reviewer** for pull requests

### Required Reviewer Configuration
- When configured as a required reviewer, PRs cannot be merged until Copilot has reviewed them
- Set at the repository level via branch protection rules:
  - Go to **Repository Settings → Branches → Branch protection rules**
  - Enable **Require review from Code Owners or specific reviewers**
  - Add Copilot as a required reviewer

### Customizing Review Standards
Use `.github/copilot-instructions.md` to provide organization-specific coding standards:
```markdown
# Copilot Review Instructions
- All functions must have docstrings
- Use our internal logging library (acme-logger) instead of print statements
- Ensure all HTTP calls include timeout parameters
- Flag any use of deprecated APIs listed in /docs/deprecated-apis.md
```

---

## Managing Feature Availability Across IDEs and github.com

### IDE-Level Controls
Admins can specify which editors have access to Copilot features:
- VS Code
- Visual Studio
- JetBrains IDEs
- Neovim
- Xcode

This is managed under **Organization Settings → Copilot → Policies → Editor settings**.

### github.com Features
Controls for Copilot features available on github.com include:
- Copilot Chat in github.com
- PR Summaries
- Copilot on mobile (github.com mobile app)
- Copilot Spaces

---

## Audit Log Events

### What is the Audit Log?
The GitHub Audit Log records significant actions taken by members within an organization. For Copilot, this includes:
- Policy changes (enabling/disabling features)
- Seat assignments (granting/revoking Copilot access)
- Content exclusion changes
- Code review policy modifications

### Accessing the Audit Log
1. Go to **Organization Settings → Security → Audit log**
2. Filter by action category: `copilot`
3. Export as JSON or CSV for analysis

### Key Copilot Audit Events

| Event | Description |
|---|---|
| `copilot.enable` | Copilot enabled for a user or team |
| `copilot.disable` | Copilot disabled for a user or team |
| `copilot.policy_update` | A Copilot policy was changed |
| `copilot.seat_assignment` | A Copilot seat was assigned |
| `copilot.seat_cancellation` | A Copilot seat was cancelled |
| `copilot.content_exclusion_update` | Content exclusion settings were changed |

### Using Audit Logs for Compliance
- Export logs periodically for compliance reporting
- Set up alerts for unauthorized policy changes
- Review logs after security incidents to trace AI-related activity

---

## Managing Subscriptions Using the REST API

### GitHub Copilot REST API
Organizations with Copilot Business or Enterprise can manage subscriptions programmatically via the REST API.

### Key API Endpoints

#### List Copilot Seat Details
```http
GET /orgs/{org}/copilot/billing/seats
Authorization: ******
```
Returns a list of all members with assigned Copilot seats, including last active time.

#### Add Users to Copilot
```http
POST /orgs/{org}/copilot/billing/selected_users
Content-Type: application/json

{
  "selected_usernames": ["octocat", "mona"]
}
```

#### Remove Users from Copilot
```http
DELETE /orgs/{org}/copilot/billing/selected_users
Content-Type: application/json

{
  "selected_usernames": ["octocat"]
}
```

#### Get Organization Copilot Settings
```http
GET /orgs/{org}/copilot/billing
Authorization: ******
```

### Required Permissions
- `manage_billing:copilot` scope for billing management
- `read:org` scope for read-only queries

### Use Cases for the REST API
- Automate seat provisioning/de-provisioning with HR systems
- Monitor seat utilization across the organization
- Build dashboards tracking Copilot adoption metrics

---

## Key Takeaways

- Organization admins have granular control over which Copilot features are available and to whom.
- Copilot Code Review can be configured as a required reviewer for pull requests.
- The Audit Log tracks all Copilot policy and seat changes for compliance purposes.
- The REST API enables programmatic management of Copilot subscriptions and policies.

---

[← Back to Features](README.md)
