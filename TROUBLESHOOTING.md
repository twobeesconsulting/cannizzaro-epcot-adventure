# Troubleshooting Guide

This guide helps resolve common issues with the EPCOT Adventure app.

## Issue: Blank Screen / Map Not Loading

### Symptom
You see "Welcome to EPCOT Adventure!" but the map area below is blank or shows an error.

### Common Causes and Solutions

#### 1. API Key Restrictions (Most Common)

**Symptom**: Console shows errors like:
```
Google Maps JavaScript API warning: NoApiKeys
Google Maps JavaScript API warning: InvalidKey
```

**Cause**: The API key is restricted to specific domains and your current domain isn't allowed.

**Solutions**:

**Option A - Use the Deployed Site** (Recommended)
- Visit the official deployed site: https://twobeesconsulting.github.io/cannizzaro-epcot-adventure/
- The API key is configured to work on this domain (both HTTP and HTTPS)

**Option B - For Local Development**
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Navigate to: APIs & Services > Credentials
3. Find the API key (or create a new one)
4. Under "Application restrictions", add:
   - `http://localhost:*`
   - `http://127.0.0.1:*`
5. Save changes and wait a few minutes for them to take effect
6. Refresh your browser

**Option C - Create Your Own Key**
1. Follow the setup instructions in [README.md](README.md)
2. Create your own Google Maps API key
3. Update the `config.js` file with your key
4. Make sure to apply proper restrictions

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

**✅ Working correctly:**
```
DOM loaded, CONFIG available: true
Script tag added to document
Google Maps API script loaded
initMap called
Map loaded successfully
```

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
