# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Add support for Rust security scanning
- Add support for Go security scanning
- CI/CD integration examples

## [1.0.0] - 2026-01-16

### Added
- Initial release of AppSec Pre-Commit Hooks
- Four security profiles:
  - `security-profile-base` - Minimal security controls
  - `security-profile-web-app` - Web application security
  - `security-profile-infra` - Infrastructure-as-Code security
  - `security-profile-mobile` - Mobile application security
- Installation script (`install.sh`) with interactive profile selection
- Comprehensive README with usage examples
- Exception process documentation

### Security Tools Included
- Gitleaks v8.18.4 - Secret detection
- Semgrep v1.78.0 - Security linting with multiple rulesets
- Bandit v1.7.9 - Python security linter
- Safety v3.2.3 - Python dependency scanner
- pre-commit-terraform v1.92.0 - Terraform security (tfsec, Checkov)
- cfn-lint v1.4.2 - CloudFormation linting
- SwiftLint v0.55.1 - Swift security linter

---

## Version Guidelines

### Major Version (X.0.0)
- Breaking changes to hook IDs or arguments
- Removal of security profiles
- Major tool version upgrades that may change behavior

### Minor Version (0.X.0)
- New security profiles added
- New tools added to existing profiles
- Non-breaking configuration changes

### Patch Version (0.0.X)
- Security tool version updates
- Bug fixes
- Documentation updates

