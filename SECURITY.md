# Security Policy for Cannizzaro Epcot Adventure

This document outlines the security approach for this project, specifically regarding the Google Maps API key.

## Table of Contents
1. About This Policy
2. Frontend API Key Security
3. Current Configuration
4. GitHub Secret Scanning Alerts
5. For Contributors
6. Reporting Vulnerabilities

---

## 1. About This Policy
This project uses a Google Maps API key to display an interactive map. As a frontend-only application, special considerations apply to API key security.

## 2. Frontend API Key Security

**Important**: This is a frontend-only application (static HTML/JavaScript). This means:

- **API keys WILL be visible** in the browser's source code and network requests
- This is **normal and expected** for frontend applications using Google Maps
- The security comes from **API key restrictions** on Google Cloud Platform, not from hiding the key

### Proper Security Approach

For frontend applications, security is achieved through:
1. **API Key Restrictions** - Limiting what the key can do and where it can be used
2. **Usage Quotas** - Setting limits to prevent abuse
3. **Monitoring** - Regular checking of usage patterns

## 3. Current Configuration

The application includes a Google Maps API key in `config.js` that has been configured with:

- **Application Restrictions**: HTTP referrer restriction to `*.twobeesconsulting.github.io/*`
- **API Restrictions**: Limited to Maps JavaScript API only
- **Purpose**: Display EPCOT location map only

This configuration allows the app to work on GitHub Pages while preventing unauthorized use.

### Why config.js is Committed

Unlike typical practice where config files are gitignored:
- This is a **public demo application** meant to work immediately when deployed
- The API key is **already restricted** to only work on the GitHub Pages domain
- Users can see a working map without needing to configure anything
- The key has minimal permissions and is monitored

## 4. GitHub Secret Scanning Alerts

**You may receive GitHub secret scanning alerts for the API key.** This is expected because:

- GitHub scans commits for patterns that look like API keys
- It cannot verify whether the key has restrictions applied
- The alerts are precautionary and don't necessarily indicate a security problem

### How to Handle These Alerts

1. **Verify the API key restrictions** in Google Cloud Console are properly configured
2. **Mark the alert** as "Won't fix" or "Used in tests" with a note about restrictions
3. **Monitor usage** regularly in Google Cloud Console
4. If you see unexpected usage, rotate the key immediately

## 5. For Contributors

If you want to customize or extend this application:

1. **To use your own API key**:
   - Create a Google Maps API key in Google Cloud Console
   - Apply proper restrictions (see Google's documentation)
   - Update `config.js` with your key
   - Test locally before committing

2. **Do not commit unrestricted API keys**:
   - Always verify restrictions are in place before committing
   - If you accidentally commit an unrestricted key, revoke it immediately
   - Create a new key with proper restrictions

3. **For local development**:
   - The committed key is restricted to GitHub Pages domain
   - To test locally, you may need to add `http://localhost:*` to the key's allowed referrers
   - Or create your own development key

## 6. Reporting Vulnerabilities

If you discover a security vulnerability or notice suspicious API usage:

1. **Do NOT** open a public issue
2. Contact the repository owner directly through GitHub
3. Provide details about the vulnerability
4. Allow time for the issue to be addressed before public disclosure

---

## Best Practices Summary

✅ **Do:**
- Use restricted API keys with HTTP referrer and API restrictions
- Monitor usage regularly in Google Cloud Console
- Set up usage quotas and billing alerts
- Document the security approach for your team

❌ **Don't:**
- Try to "hide" API keys in frontend code (it's impossible)
- Commit unrestricted API keys to any repository
- Ignore unusual usage patterns
- Share API keys across multiple unrelated projects
   - Maps JavaScript API
   - Places API
   - (Only enable what you actually use)

3. **Set quotas and alerts**
   - Configure daily usage limits
   - Set up billing alerts
   - Monitor usage regularly

### .env Files (Alternative Approach)
For server-side applications, use `.env` files:
- Keep your API keys and secrets in a local `.env` file only
- Ensure `.env` (and similar secret files) are included in `.gitignore`

Example `.env` file (see `.env.example`):
```
GOOGLE_API_KEY=your-google-api-key-here
```

### Using Secret Managers
For production environments, consider:
- [Google Secret Manager](https://cloud.google.com/secret-manager/docs)
- [GitHub Actions Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- Backend proxy services to hide API keys completely

## 5. Workflow for Contributors
- Request API key access from project maintainers – never share by email or public chat
- Never paste or expose credentials in issue trackers, PRs, or logs
- Use `config.example.js` to show expected configuration to contributors (never put real values)
- Review all commits for accidental exposure before pushing
- **Always** verify API restrictions are properly configured

## 6. Key Rotation Procedure
- If exposure is suspected or restrictions were not properly set, immediately revoke and regenerate the API key
- Apply proper restrictions to the new key BEFORE using it
- Update all deployment and CI secrets as needed
- Communicate key rotations to affected team members privately

## 7. Reporting Vulnerabilities
If you discover a vulnerability in credential handling or anything else in this repository, please contact a maintainer privately to disclose it responsibly.

---
**Secure coding saves time and risk—thank you for following these practices!**