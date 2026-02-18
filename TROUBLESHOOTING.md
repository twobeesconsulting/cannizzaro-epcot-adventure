# Troubleshooting Guide

This guide helps resolve common issues with the EPCOT Adventure app.

## Understanding Console Errors

When you see errors in the browser console, they usually indicate one of the following issues:

### Expected Errors (When Testing Locally or on Unauthorized Domains)

**These are NORMAL and EXPECTED when not on the authorized domain:**

```
Google Maps JavaScript API warning: NoApiKeys
Google Maps JavaScript API warning: InvalidKey
```

**Why?** The API key in this repository is restricted to work ONLY on `twobeesconsulting.github.io` for security reasons. This is intentional and follows best practices.

**Solution:** 
- Visit the official site: https://twobeesconsulting.github.io/cannizzaro-epcot-adventure/
- OR create your own API key for local testing (see below)

### Other Console Messages You Might See

```
Google Maps JavaScript API has been loaded directly without loading=async
```
**This is informational only** - The app already loads the API asynchronously using the `async` and `defer` attributes.

## Issue: Blank Screen / Map Not Loading

### Symptom
You see "Welcome to EPCOT Adventure!" but the map area shows an error message.

### Common Causes and Solutions

#### 1. API Key Domain Restrictions (Most Common)

**Symptom**: You see a pink/red error box saying "Google Maps API Key Restricted"

**Cause**: The API key is restricted to `twobeesconsulting.github.io` domain only.

**This is WORKING AS INTENDED for security!**

**Solutions**:

**Option A - Use the Deployed Site** (Recommended)
- Visit: https://twobeesconsulting.github.io/cannizzaro-epcot-adventure/
- The map will work perfectly on this domain

**Option B - For Local Development**
- Create your own Google Maps API key (free for testing)
- Update `config.js` with your key
- Your key can allow `localhost` and other domains

**Option C - Add localhost to existing key** (If you manage the key)
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Navigate to: APIs & Services > Credentials
3. Find the API key
4. Under "Application restrictions", add:
   - `http://localhost:*`
   - `http://127.0.0.1:*`
5. Save changes and wait a few minutes
6. Refresh your browser

#### 2. Config File Issues

**Symptom**: Console shows:
```
Uncaught SyntaxError: Unexpected token 'export'
CONFIG is not defined
```

**Cause**: The `config.js` file has incorrect format or isn't loading.

**Solution**:
1. Open `config.js` in a text editor
2. Ensure it looks exactly like this (no `export` statements):
   ```javascript
   const CONFIG = {
     GOOGLE_MAPS_API_KEY: 'your-api-key-here'
   };
   ```
3. If it has `export default` or other module syntax, remove it
4. Save and refresh your browser

#### 3. Browser Ad Blockers / Extensions

**Symptom**: Map doesn't load even though everything else seems correct.

**Cause**: Browser extensions blocking Google Maps API.

**Solution**:
1. Try opening the page in an incognito/private window
2. Temporarily disable ad blockers or privacy extensions
3. Add an exception for the site in your blocker
4. Try a different browser

#### 4. Internet Connection / Firewall

**Symptom**: No errors in console, but map area remains empty.

**Cause**: Network blocking access to Google's servers.

**Solution**:
1. Check your internet connection
2. Try accessing https://maps.googleapis.com/maps/api/js in your browser
3. Check if your firewall is blocking Google services
4. Try a different network (mobile hotspot, different WiFi)

#### 5. Cache Issues

**Symptom**: Map was working before, now it's not.

**Solution**:
1. Hard refresh the page:
   - Windows/Linux: `Ctrl + F5` or `Ctrl + Shift + R`
   - Mac: `Cmd + Shift + R`
2. Clear browser cache for the site
3. Close and reopen your browser

## Checking Browser Console

To see detailed error messages:

**Chrome/Edge/Brave:**
1. Press `F12` or right-click and select "Inspect"
2. Click the "Console" tab
3. Look for red error messages

**Firefox:**
1. Press `F12` or right-click and select "Inspect Element"
2. Click the "Console" tab
3. Look for red error messages

**Safari:**
1. Enable developer tools: Safari > Preferences > Advanced > Show Develop menu
2. Press `Cmd + Option + C` or Develop > Show JavaScript Console
3. Look for error messages

## Still Having Issues?

If none of the above solutions work:

1. **Check the console for errors** and note the exact error messages
2. **Take a screenshot** of the error and the page
3. **Open an issue** on the GitHub repository with:
   - Description of the problem
   - Screenshots
   - Console errors
   - Browser and version you're using
   - Whether you're running locally or on deployed site

## Quick Reference: Expected Console Messages

**✅ Working correctly on authorized domain (GitHub Pages):**
```
DOM loaded, CONFIG available: true
Script tag added to document
Google Maps API script loaded
initMap called
Map loaded successfully
```

**⚠️ EXPECTED on unauthorized domains (localhost, etc.):**
```
DOM loaded, CONFIG available: true
Not on authorized domain. Map may not load due to API key restrictions.
Script tag added to document
Failed to load Google Maps API
Google Maps JavaScript API warning: NoApiKeys
Google Maps JavaScript API warning: InvalidKey
```
→ This is NORMAL! Visit the deployed site or create your own API key

**ℹ️ Informational (can be ignored):**
```
Google Maps JavaScript API has been loaded directly without loading=async
```
→ The app already loads asynchronously - this warning can be safely ignored

**❌ Config missing:**
```
CONFIG is not defined. Please ensure config.js is loaded.
```
→ Check that config.js exists and is properly formatted

**❌ API key issue:**
```
Google Maps JavaScript API warning: NoApiKeys
Google Maps JavaScript API warning: InvalidKey
```
→ Check API key restrictions in Google Cloud Console

**❌ Network issue:**
```
Failed to load resource: net::ERR_BLOCKED_BY_CLIENT
```
→ Check browser extensions/ad blockers
