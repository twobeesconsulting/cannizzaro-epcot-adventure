# Google Maps API Link - How to Add It Back

## The Direct Answer

The Google Maps API link that was removed from the code is:

```
https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY_HERE&libraries=places
```

## Why Was It Removed?

The hardcoded API link was removed from `index.html` (line 10) for security reasons. It's now loaded **dynamically** from a local configuration file.

## How to Add It Back (Correct Way)

### Step 1: Get a Google Maps API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Enable these APIs:
   - Maps JavaScript API
   - Places API
4. Go to **APIs & Services → Credentials**
5. Click **Create Credentials → API Key**
6. **Important**: Restrict your key (see restrictions below)

### Step 2: Set Up Your Local Config File

```bash
# Copy the example file to create your config
cp config.example.js config.js
```

### Step 3: Add Your API Key

Edit `config.js` and replace `YOUR_API_KEY_HERE` with your actual key:

```javascript
const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'AIzaSyBcgyqnX0qKID5n...'  // Your real key here
};
```

### Step 4: Open the Application

Simply open `index.html` in your browser. The API will be loaded automatically from your `config.js` file.

## Required API Key Restrictions

**IMPORTANT**: To protect your API key, apply these restrictions in Google Cloud Console:

### Application Restrictions
- **HTTP referrers**: Add your domain(s)
  - For local testing: `http://localhost/*` or `file:///*`
  - For production: `https://yourdomain.com/*`

### API Restrictions
- ✅ **Maps JavaScript API** (required)
- ✅ **Places API** (required)
- ❌ Disable all other APIs

### Billing & Usage
- Set daily usage limits
- Enable billing alerts
- Monitor usage regularly

## How It Works Now

The application loads the Google Maps API dynamically at runtime:

```javascript
// In index.html around line 1212
const script = document.createElement('script');
script.src = `https://maps.googleapis.com/maps/api/js?key=${apiKey}&libraries=places`;
document.head.appendChild(script);
```

Your `config.js` file provides the `apiKey` variable, and the script creates and loads the Google Maps API link automatically.

## Troubleshooting

### "Failed to load Google Maps"
**Cause**: Missing or invalid API key  
**Fix**: Make sure `config.js` exists and has a valid key

### Map shows but doesn't work
**Cause**: API restrictions too tight  
**Fix**: Check that Maps JavaScript API and Places API are enabled

### GitHub security alerts
**Cause**: Frontend apps expose API keys in browser  
**Fix**: This is normal - the key restrictions provide security

## Why This Approach Is Better

| Old Way | New Way |
|---------|---------|
| ❌ API key in HTML (committed to Git) | ✅ API key in `config.js` (gitignored) |
| ❌ Everyone sees your key | ✅ Each person uses their own key |
| ❌ Hard to change | ✅ Easy to update locally |

## Related Documentation

- **Setup Guide**: [QUICKSTART.md](QUICKSTART.md)
- **Security Info**: [SECURITY.md](SECURITY.md)
- **Config FAQ**: [CONFIG_FAQ.md](CONFIG_FAQ.md)
- **Visual Guide**: [CONFIG_VISUAL_GUIDE.md](CONFIG_VISUAL_GUIDE.md)

## Quick Reference

```bash
# One-time setup
cp config.example.js config.js

# Edit config.js and add your key
# Then just open index.html - it works!
```

**The map will now work with your own restricted Google Maps API key!**
