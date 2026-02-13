# Security Policy for Cannizzaro Epcot Adventure

This document outlines best practices and required steps for securing sensitive credentials—especially Google API keys—used in this project.

## Table of Contents
1. About This Policy
2. Frontend API Key Considerations
3. GitHub Secret Scanning Alerts
4. Secure Credential Handling
   - Storing API Keys
   - .env files and config.js
   - Secret Managers
5. Workflow for Contributors
6. Key Rotation Procedure
7. Reporting Vulnerabilities

---

## 1. About This Policy
Protecting sensitive credentials is critical to the integrity and security of the application and user data. Public exposure can lead to data theft, app abuse, and other breaches.

## 2. Frontend API Key Considerations

**Important**: This is a frontend-only application (static HTML/JavaScript). This means:

- **API keys WILL be visible** in the browser's source code and network requests
- This is **normal and expected** for frontend applications using Google Maps
- The security comes from **API key restrictions** on Google Cloud Platform, not from hiding the key

### Proper Security Approach

Instead of trying to hide the API key (which is impossible in a frontend app), we:
1. Use a **restricted API key** with proper limitations
2. Keep the config file in `.gitignore` to avoid committing it
3. Document proper restrictions for contributors

## 3. GitHub Secret Scanning Alerts

**You may continue to receive GitHub secret scanning alerts even with proper restrictions in place.** This is expected behavior because:

- GitHub scans commits for patterns that look like API keys
- It cannot verify whether the key has restrictions applied
- The alerts are precautionary and don't necessarily indicate a security problem

### How to Handle These Alerts

1. **Verify your API key restrictions** in Google Cloud Console:
   - Go to APIs & Services > Credentials
   - Check that your key has Application restrictions (HTTP referrers)
   - Confirm API restrictions are set to only Maps JavaScript API and Places API
   - Ensure usage limits are configured

2. **If restrictions are properly configured**, you can:
   - Mark the GitHub alert as "resolved" or "false positive"
   - Document in your team that the key is restricted
   - Continue monitoring usage in Google Cloud Console

3. **To eliminate future alerts**, consider:
   - Using a backend proxy service to completely hide the API key
   - Using a serverless function (e.g., Netlify Functions, Cloudflare Workers)
   - Note: This adds complexity and may not be necessary if restrictions are properly set

## 4. Secure Credential Handling
## 4. Secure Credential Handling

### Risks of Exposed Credentials
- Unexpected usage and billing charges
- Unauthorized access to APIs and data
- Compromised user trust and legal risk

### Storing API Keys
- **Never** commit API keys or secrets to git without restrictions in place
- Use environment variables or config files to store sensitive data
- Prefer managed secret storage solutions for production
- **Always** apply proper API restrictions in Google Cloud Console

### config.js Files
- Keep your API keys and secrets in a local `config.js` file only
- Ensure `config.js` is included in `.gitignore`
- Use `config.example.js` as a template for contributors

Example `config.js` file (see `config.example.js`):
```javascript
const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'your-google-api-key-here'
};
```

### Google Maps API Key Restrictions

**Required restrictions for Google Maps API keys:**

1. **Application restrictions** → HTTP referrers (websites)
   - Add your domain(s): `https://yourdomain.com/*`
   - For local development: `http://localhost:*`

2. **API restrictions** → Restrict key to specific APIs
   - Maps JavaScript API
   - Places API
   - (Only enable what you actually use)

3. **Set quotas and alerts**
   - Configure daily usage limits
   - Set up billing alerts
   - Monitor usage regularly

### .env Files (Alternative Approach)

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