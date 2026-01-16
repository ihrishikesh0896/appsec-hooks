# AppSec Pre-Commit Hooks

Centralized security controls for all repositories. Managed by the AppSec team.

> **Move from advisory to authoritative security by treating your controls as a platform, not a suggestion.**

## 🚀 Quick Start

### One-Line Installation

```bash
curl -sSL https://raw.githubusercontent.com/ihrishikesh0896/appsec-hooks/main/install.sh | bash
```

### Manual Installation

1. Add to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/ihrishikesh0896/appsec-hooks
    rev: v1.0.0  # Use latest tagged version
    hooks:
      - id: security-profile-web-app  # Choose your profile
```

2. Install the hooks:

```bash
pre-commit install
```

## 📋 Available Profiles

| Profile | ID | Use Case | Tools Included |
|---------|-----|----------|----------------|
| **Base** | `security-profile-base` | All repositories | Gitleaks, Semgrep (secrets & security-audit) |
| **Web App** | `security-profile-web-app` | Web applications | + OWASP Top 10, XSS, SQLi, Bandit, Safety |
| **Infra** | `security-profile-infra` | Infrastructure-as-Code | + tfsec, Checkov, cfn-lint, K8s rules |
| **Mobile** | `security-profile-mobile` | Mobile apps | + MobSF rules, SwiftLint |

### Profile Details

#### Base Profile (`security-profile-base`)
Minimal security controls suitable for all repositories:
- **Gitleaks** - Secret detection
- **Semgrep** - Security audit and secret patterns
- **Pre-commit hooks** - Private key detection, large file checks

#### Web Application Profile (`security-profile-web-app`)
Comprehensive security for web applications:
- Everything in Base, plus:
- **OWASP Top 10** rules via Semgrep
- **XSS** detection
- **SQL Injection** detection
- **Bandit** - Python security linter
- **Safety** - Python dependency vulnerability scanner

#### Infrastructure Profile (`security-profile-infra`)
Security controls for Infrastructure-as-Code:
- Everything in Base, plus:
- **tfsec** - Terraform security scanner
- **Checkov** - IaC security scanner
- **cfn-lint** - CloudFormation linter
- **Kubernetes** rules via Semgrep

#### Mobile Profile (`security-profile-mobile`)
Security controls for mobile applications:
- Everything in Base, plus:
- **MobSF** rules via Semgrep
- **SwiftLint** - Swift security linter (iOS)

## 🔧 Multi-Profile Configuration

For projects that span multiple domains (e.g., a web app with infrastructure code):

```yaml
# .pre-commit-config.yaml
repos:
  # Primary: Web Application Security Profile
  - repo: https://github.com/ihrishikesh0896/appsec-hooks
    rev: v1.0.0
    hooks:
      - id: security-profile-web-app
        stages: [commit]

  # Secondary: Run infra checks only on IaC files
  - repo: https://github.com/ihrishikesh0896/appsec-hooks
    rev: v1.0.0
    hooks:
      - id: security-profile-infra
        files: ^(terraform/|k8s/|cloudformation/|\.github/)
        stages: [commit]
```

## ⚠️ Exception Process

If a security rule is blocking a legitimate use case:

1. **Do NOT disable the hook** in your repository
2. **Document the issue** in a Jira ticket (APPSEC project)
3. **Request an exception** with:
   - Business justification
   - Risk assessment
   - Proposed mitigation
   - Expiration date
4. **Get approval** from AppSec team and project leadership

Exceptions are:
- ✅ Temporary and time-bound
- ✅ Documented and auditable
- ✅ Risk-accepted with compensating controls
- ❌ Never permanent opt-outs

## 📦 Versioning

> **⚠️ Golden Rule: Never point to `main` branch**

```yaml
# ❌ WRONG - Breaking changes can halt commits company-wide
rev: main

# ✅ CORRECT - Version-pinned for stability
rev: v1.0.0
```

### Updating Hooks

**Manual update:**
```bash
pre-commit autoupdate
```

**Automated with Dependabot:** Add to `.github/dependabot.yml`:
```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

## 🛠️ Useful Commands

```bash
# Run all hooks on all files
pre-commit run --all-files

# Run specific hook
pre-commit run gitleaks --all-files

# Update hook versions
pre-commit autoupdate

# Skip hooks temporarily (emergency only!)
git commit --no-verify -m "emergency fix"

# Clear pre-commit cache
pre-commit clean
```

## 📊 Compliance & Auditing

With centralized hooks, you can confidently state:
- ✅ Every repository enforces the same security controls
- ✅ All changes are version-controlled and auditable
- ✅ Security updates propagate automatically
- ✅ Exceptions are documented and time-bound

## 🆘 Support

- **Slack:** #appsec-support
- **Jira:** APPSEC project
- **Documentation:** [Internal Wiki Link]

## 📝 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for version history.

---

*Maintained by the Application Security Team*

