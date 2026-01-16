# AppSec Hooks

This repository provides a centralized collection of pre-commit hooks to enforce security best practices across your projects.

## Usage

To use these hooks in your project, add the following to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/ihrishikesh0896/appsec-hooks
    rev: main # or a specific tag
    hooks:
      - id: corporate-security-critical
      # Or, use individual hooks:
      # - id: gitleaks
      # - id: semgrep-sast
      # - id: checkov-iac
```

### Dependencies

This repository uses `language: golang` and `language: python` for the hooks. `pre-commit` will automatically handle the installation of the necessary tools (Gitleaks, Semgrep, Checkov) in isolated environments. You do not need to install them manually.

### Hooks

- **gitleaks**: Scans for hardcoded secrets.
- **semgrep-sast**: Performs static analysis for security vulnerabilities.
- **checkov-iac**: Scans infrastructure as code for misconfigurations.
- **corporate-security-critical**: A "meta" hook that runs a combination of the most critical security checks (currently Gitleaks and Semgrep).

### How it Works for a Beginner Developer

1.  **Install pre-commit:**
    ```bash
    pip install pre-commit
    ```

2.  **Create a `.pre-commit-config.yaml` file** in the root of your project with the content from the "Usage" section above.

3.  **Install the git hooks:**
    ```bash
    pre-commit install
    ```

Now, every time you run `git commit`, the security hooks will automatically run. If any issues are found, the commit will be aborted, and the errors will be displayed in your terminal. You can then fix the issues and re-commit your changes.
