# Security Exception Process

## Overview

This document outlines the formal process for requesting exceptions to security controls enforced by the AppSec Pre-Commit Hooks.

## Key Principles

1. **No Permanent Opt-Outs** - Exceptions are temporary, risk-accepted deviations
2. **Documented and Approved** - Every exception must be formally documented
3. **Time-Bound** - Every exception has an expiration date
4. **Compensating Controls** - Alternative mitigations must be in place

## When to Request an Exception

Request an exception when:
- A security rule produces a false positive that cannot be resolved
- A legitimate use case is blocked by a security control
- A third-party dependency triggers security warnings that cannot be updated

**Do NOT request an exception when:**
- You want to skip security checks for convenience
- You haven't investigated the root cause of the finding
- A fix is available but would take "too long"

## Exception Request Process

### Step 1: Investigate the Finding

Before requesting an exception:
1. Understand what the security tool is detecting
2. Verify if it's a true positive or false positive
3. Explore if there's a secure alternative implementation
4. Check if the issue can be resolved with inline suppressions

### Step 2: Create a Jira Ticket

Create a ticket in the **APPSEC** project with:

**Title:** `[Exception Request] <Tool Name> - <Brief Description>`

**Required Information:**
```
## Repository
<repository-name>

## Security Tool
<tool-name> (e.g., Semgrep, Gitleaks, Bandit)

## Rule/Finding ID
<rule-id>

## Description of Finding
<What is the tool detecting?>

## Business Justification
<Why is an exception needed?>

## Risk Assessment
- Likelihood: <Low/Medium/High>
- Impact: <Low/Medium/High>
- Overall Risk: <Low/Medium/High>

## Proposed Compensating Controls
<What alternative security measures will be in place?>

## Requested Duration
<How long is the exception needed?>

## Remediation Plan
<What is the plan to eliminate the need for this exception?>
```

### Step 3: Approval Process

1. **AppSec Team Review** - Security engineer reviews the request
2. **Risk Assessment** - Formal risk evaluation
3. **Leadership Approval** - Project/team lead must approve
4. **Documentation** - Exception is recorded in the exception registry

### Step 4: Implementation

Once approved:
1. AppSec team provides inline suppression syntax
2. Developer implements suppression with tracking comment
3. Exception is added to monitoring dashboard
4. Calendar reminder set for expiration review

## Inline Suppression Format

When an exception is approved, use this format:

```python
# SECURITY-EXCEPTION: APPSEC-1234 (expires: 2026-06-30)
# Reason: False positive - variable name contains 'password' but is not a credential
password_field_name = "user_password"  # nosec B105
```

```yaml
# SECURITY-EXCEPTION: APPSEC-1234 (expires: 2026-06-30)
# Reason: Test fixture containing dummy credentials
test_api_key: "test-key-12345"  # gitleaks:allow
```

## Exception Registry

All approved exceptions are tracked in:
- **Jira:** APPSEC project with `exception` label
- **Dashboard:** [Internal Security Dashboard Link]
- **Quarterly Review:** All exceptions reviewed every quarter

## Expiration and Renewal

- Exceptions are reviewed 2 weeks before expiration
- Renewal requires re-justification and re-approval
- Expired exceptions without renewal will cause CI failures

## Escalation Path

If your exception request is denied:
1. Discuss with AppSec team to understand concerns
2. Escalate to AppSec Lead if needed
3. Final escalation to CISO for business-critical issues

## Contact

- **Slack:** #appsec-support
- **Email:** appsec@company.com
- **Jira:** APPSEC project

---

*This process ensures that security risks are consciously accepted, not silently ignored.*

