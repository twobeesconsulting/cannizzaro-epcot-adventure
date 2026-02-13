# Addressing Google API Key Alerts

This document explains the changes made to address Google API key security concerns and how to handle ongoing alerts.

## Changes Made

### 1. API Key Extraction (✅ Completed)
- **Removed** hardcoded API key from `index.html`
- **Created** `config.js` to store API keys (gitignored)
- **Created** `config.example.js` as a template for contributors
- **Added** dynamic loading of Google Maps API from config
- **Updated** `.gitignore` to exclude `config.js`

### 2. Enhanced Map Interactions (✅ Completed)
- **Made challenge list items clickable** - clicking any challenge in the list now:
  - Switches to the Map tab
  - Centers the map on that location
  - Opens the info window for that challenge
  - Allows checking/unchecking from either the list or the map
- **Verified "Next Up" marker is clickable** - the bouncing marker has always been clickable
  - Click the bouncing orange marker to see details
  - The info window will appear with challenge details and a checkbox

### 3. Documentation Updates (✅ Completed)
- **README.md**: Added setup instructions and API key guidance
- **SECURITY.md**: Comprehensive security documentation explaining:
  - Why frontend apps expose API keys
  - How to properly restrict API keys on Google Cloud
  - Why GitHub alerts may continue even with restrictions
  - Proper workflow for contributors

## Understanding GitHub Secret Scanning Alerts

**Important**: GitHub's secret scanning will continue to alert on the API key in git history even after these changes. This is **expected behavior**.

### Why Alerts Continue

1. **Git History**: The API key exists in previous commits and will always be there unless you rewrite history (not recommended for shared repositories)
2. **GitHub Scanner**: Cannot verify if a key has restrictions applied - it only detects patterns
3. **Frontend Apps**: API keys are inherently visible in browser source code and network requests

### Is This a Security Problem?

**No**, if you have properly configured API key restrictions on Google Cloud Platform:

#### Required Restrictions Checklist
- [ ] **Application restrictions** → HTTP referrers (websites)
  - Add your production domain(s)
  - Add `http://localhost:*` for local development
- [ ] **API restrictions** → Limit to specific APIs
  - Maps JavaScript API
  - Places API
  - Remove any other APIs you don't use
- [ ] **Usage quotas** → Set daily limits
- [ ] **Billing alerts** → Configure in Google Cloud Console

### How to Handle the Alerts

#### Option 1: Keep Current Key (Recommended if properly restricted)
1. ✅ Verify all restrictions are properly configured (see checklist above)
2. ✅ Mark GitHub alert as "Won't fix" or "False positive"
3. ✅ Add a comment explaining the key has proper restrictions
4. ✅ Monitor usage regularly in Google Cloud Console

#### Option 2: Rotate to a New Key (If restrictions weren't set before)
1. Create a new Google Maps API key in Google Cloud Console
2. Apply ALL restrictions BEFORE using it (see checklist above)
3. Update `config.js` with the new key
4. Delete the old key from Google Cloud Console
5. Mark GitHub alert as resolved

#### Option 3: Complete History Cleanup (Most disruptive, rarely needed)
If you absolutely must remove the key from git history:
1. Rotate to a new key first (Option 2)
2. Use `git filter-branch` or `BFG Repo-Cleaner` to remove from history
3. Force push to all branches
4. All collaborators must re-clone the repository
5. **Note**: This is disruptive and usually not necessary if restrictions are proper

## Testing the Changes

### Test API Key Loading
1. Copy `config.example.js` to `config.js`
2. Add your API key to `config.js`
3. Open `index.html` in a browser
4. The map should load correctly
5. If you see an error, check that `config.js` exists and has the correct format

### Test Challenge List Click Navigation
1. Open the app and go to the Challenge List tab
2. Click on any challenge card (not just the checkbox)
3. The app should:
   - Switch to the Map tab
   - Center on that challenge's location
   - Open an info window showing challenge details
   - You can check/uncheck from the info window

### Test "Next Up" Marker
1. Open the app with no progress (or reset progress)
2. Go to the Map tab
3. You should see an orange bouncing marker (this is "next up")
4. Click the bouncing marker
5. An info window should open with challenge details

## Best Practices Going Forward

1. **Never commit** `config.js` - it's in `.gitignore`
2. **Always verify** new API keys have restrictions before use
3. **Monitor usage** in Google Cloud Console regularly
4. **Share** `config.example.js` with new contributors
5. **Document** any changes to required API access

## Questions?

If you have questions about:
- API key restrictions → See [Google Cloud API Key Best Practices](https://cloud.google.com/docs/authentication/api-keys)
- GitHub alerts → See [About secret scanning](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning)
- This implementation → Open an issue in the repository

---

**Summary**: The application is now configured to use external API key configuration, challenge list items are clickable for map navigation, and comprehensive documentation explains why alerts may continue and how to handle them properly.
