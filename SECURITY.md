# Security Policy for Cannizzaro Epcot Adventure

This document outlines best practices and required steps for securing sensitive credentials—especially Google API keys—used in this project.

## Table of Contents
1. About This Policy
2. Risks of Exposed Credentials
3. Secure Credential Handling
   - Storing API Keys
   - .env files
   - Secret Managers
4. Workflow for Contributors
5. Key Rotation Procedure
6. Reporting Vulnerabilities

---

## 1. About This Policy
Protecting sensitive credentials is critical to the integrity and security of the application and user data. Public exposure can lead to data theft, app abuse, and other breaches.

## 2. Risks of Exposed Credentials
- Unexpected usage and billing charges
- Unauthorized access to APIs and data
- Compromised user trust and legal risk

## 3. Secure Credential Handling
### Storing API Keys
- **Never** commit API keys or secrets to git.
- Use environment variables to store sensitive data.
- Prefer managed secret storage solutions for production.

### .env Files
- Keep your API keys and secrets in a local `.env` file only.
- Ensure `.env` (and similar secret files) are included in `.gitignore`.

Example `.env` file (see `.env.example`):

### Using Secret Managers
- [Google Secret Manager](https://cloud.google.com/secret-manager/docs)
- [GitHub Actions Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

## 4. Workflow for Contributors
- Request API key access from project maintainers – never share by email or public chat.
- Never paste or expose credentials in issue trackers, PRs, or logs.
- Use `.env.example` to show expected secrets to contributors (never put real values).
- Review all commits for accidental exposure before pushing.

## 5. Key Rotation Procedure
- If exposure is suspected, immediately revoke and regenerate the API key.
- Update all deployment and CI secrets as needed.
- Communicate key rotations to affected team members privately.

## 6. Reporting Vulnerabilities
If you discover a vulnerability in credential handling or anything else in this repository, please contact a maintainer privately to disclose it responsibly.

---
**Secure coding saves time and risk—thank you for following these practices!**
