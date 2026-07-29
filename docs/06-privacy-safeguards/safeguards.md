# Applying Safeguards and Troubleshooting

This section covers how to enable key safeguards in GitHub Copilot and how to troubleshoot common issues.

---

## Enabling Suggestions Matching Public Code Filtering

### What Is the Public Code Filter?
The "Suggestions matching public code" filter detects when a Copilot suggestion closely matches publicly available code (typically ≥150 consecutive characters that match a known public code repository).

### Why Enable It?
- **License compliance**: Matching code may carry open-source licenses (GPL, LGPL, etc.) that impose conditions
- **IP protection**: Ensures generated code is not inadvertently reproducing third-party copyrighted code
- **Legal risk reduction**: Reduces exposure in regulated industries or with strict IP requirements

### How to Enable the Filter

#### Organization Level (Admins)
1. Go to **Organization Settings → Copilot → Policies**
2. Find **"Suggestions matching public code"**
3. Set to **Blocked** (to filter out matching suggestions)

#### Individual Level
1. Go to **GitHub.com → Settings → Copilot**
2. Find **"Suggestions matching public code"**
3. Set to **Blocked**

> **Note**: Organization policies override individual settings. If the organization blocks matching code, individuals cannot override this.

### When "Allowed" Is Appropriate
Some organizations choose to **Allow** suggestions matching public code because:
- They have legal processes to review license compliance separately
- They work exclusively with permissive-licensed code (MIT, Apache)
- Filtering reduces the quality/quantity of suggestions too much for their workflow

---

## Resolving Issues with Suggestions

### Issue: Copilot Is Not Showing Suggestions

**Check 1: Is Copilot enabled?**
- Look for the Copilot icon in the IDE status bar
- If the icon shows a slash, Copilot is disabled globally or for the current language
- Click the icon to enable it, or check settings

**Check 2: Is the file excluded?**
- Check if the current file matches a content exclusion pattern
- Verify in **Repository Settings → Copilot → Content exclusion**
- Check organization-level exclusions as well

**Check 3: Is the language disabled?**
- In VS Code: check `"github.copilot.enable"` in settings
- Ensure the current file's language is set to `true`

**Check 4: Is your subscription active?**
- Visit **GitHub.com → Settings → Copilot** to confirm subscription status
- If using an organization plan, confirm your organization admin has granted you access

**Check 5: Are you authenticated?**
- Use the command palette: `GitHub Copilot: Sign In`
- Ensure your GitHub account matches the one with the active subscription

**Check 6: Network or proxy issues?**
- Copilot requires outbound HTTPS connections to GitHub's proxy
- Corporate firewalls may block `copilot-proxy.githubusercontent.com`
- Check with your network admin if you are on a corporate network

---

### Issue: Content Exclusions Are Not Working

**Symptom**: Copilot still suggests code from excluded files.

**Troubleshooting Steps**:
1. Verify the glob pattern syntax is correct
   - Patterns are case-sensitive on Linux/macOS
   - Use `**/` prefix for patterns that should match in any directory
2. Confirm the exclusion was saved (look for a success confirmation in settings)
3. Restart the IDE to refresh exclusion settings
4. Check both repository-level and organization-level exclusions for conflicts
5. Use the Copilot extension's diagnostic tool (if available) to confirm exclusion status

**Testing an Exclusion**:
- Open an excluded file
- Look for the Copilot icon with a slash in the status bar
- This confirms the file is recognized as excluded

---

### Issue: Suggestions Are Low Quality or Irrelevant

**Possible Causes and Solutions**:

| Cause | Solution |
|---|---|
| Insufficient context | Open relevant files in other tabs |
| Vague or sparse comments | Write more descriptive comments or use Chat |
| Conflicting context | Close unrelated files |
| Language/framework mismatch | Specify the framework explicitly in comments or Chat |
| Long conversation history | Start a new Chat session |

---

### Issue: Copilot Is Suggesting Sensitive Code

**If Copilot suggests code from a file that should be excluded**:
1. Immediately report via the thumbs-down button
2. Verify content exclusion configuration (see above)
3. Check for potential configuration drift (recent policy changes)
4. Escalate to the organization admin if exclusions are configured but not enforced

---

## Content Exclusion Troubleshooting Checklist

```
□ Is the file path correct relative to the repository root?
□ Is the glob pattern using the correct syntax? (** for recursive, * for single-level)
□ Are there any typos in the pattern?
□ Is the exclusion saved at the correct level (repo vs. org)?
□ Has the IDE been restarted after the exclusion was configured?
□ Is the Copilot extension updated to the latest version?
□ Do organization-level exclusions override the expected behavior?
```

---

## Safeguards Summary

| Safeguard | What It Protects | Where to Configure |
|---|---|---|
| Content exclusions | Sensitive files from becoming context | Repository Settings or Org Settings |
| Public code matching filter | License and IP risks | Org Settings or Personal Settings |
| Training data opt-out | User code from being used for training | Personal Settings (Individual) or Org Policy (Business/Enterprise) |
| Organization policies | Feature availability and compliance | Organization Settings → Copilot |
| Secret scanning | Hard-coded secrets in code | GitHub Repository Settings |
| Code scanning (CodeQL) | Security vulnerabilities in generated code | GitHub Repository Settings → Security |

---

## Key Takeaways

- The public code matching filter reduces license risk and should be enabled for most commercial projects.
- Common Copilot issues are diagnosable by checking: subscription status, file exclusions, language settings, authentication, and network connectivity.
- Content exclusion issues are often due to incorrect glob patterns or caching—verify patterns and restart the IDE.
- Multiple safeguards should be layered for comprehensive protection: content exclusions + public code filter + training opt-out + security scanning.

---

[← Back to Privacy and Safeguards](README.md)
