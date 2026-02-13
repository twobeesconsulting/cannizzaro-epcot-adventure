# Quick Start Guide for Users

This guide helps you get the updated application running after the recent changes.

## What Changed?

Three issues were fixed:
1. ✅ **API Key Security**: Key moved to separate config file
2. ✅ **Interactive Challenge List**: Click challenges to see them on the map
3. ✅ **Bouncing Marker**: Already clickable (was working correctly)

## Setup Steps (First Time)

### 1. Copy the Config File
```bash
cp config.example.js config.js
```

### 2. Add Your Google Maps API Key
Edit `config.js` and replace `YOUR_API_KEY_HERE` with your actual key:
```javascript
const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'AIzaSy...'  // Your actual key here
};
```

### 3. Open the Application
Simply open `index.html` in your browser or serve it with:
```bash
python3 -m http.server 8080
# Then visit http://localhost:8080
```

## New Features

### Click Challenge to See Location
- Open the **Challenge List** tab
- Click on any challenge card
- The map will automatically:
  - Switch to Map tab
  - Center on that location
  - Show an info window with details
  - Let you check it off right there!

### Check Boxes from Map or List
- Check boxes in the Challenge List OR
- Check boxes in the map info windows
- Both work the same way!

### Bouncing "Next Up" Marker
- The orange bouncing marker shows your next challenge
- Click it to see what's next!
- It has always been clickable

## About the GitHub Alerts

**You may still see GitHub secret scanning alerts.** This is normal!

### Why?
- The API key is in the git history (old commits)
- GitHub can't tell if it's restricted or not
- Frontend apps always expose API keys to browsers

### Is This a Problem?
**No, IF you have proper restrictions!**

### Check Your Restrictions
Go to [Google Cloud Console](https://console.cloud.google.com/):
1. APIs & Services → Credentials
2. Click your API key
3. Verify these are set:

**Application Restrictions**:
- ✅ HTTP referrers
- Add your domain: `https://yourdomain.com/*`
- Add for local: `http://localhost:*`

**API Restrictions**:
- ✅ Restrict key
- ✅ Maps JavaScript API
- ✅ Places API
- ❌ Nothing else

**Quotas & Alerts**:
- ✅ Set daily usage limits
- ✅ Configure billing alerts

### Handling the Alert

**Option A: Mark as False Positive** (Recommended)
1. Go to the GitHub security alert
2. Click "Dismiss alert"
3. Select "False positive" or "Won't fix"
4. Add comment: "Key has proper restrictions on Google Cloud"
5. Continue monitoring usage in Google Cloud Console

**Option B: Rotate to New Key**
1. Create new key in Google Cloud Console
2. Apply ALL restrictions BEFORE using it
3. Update `config.js` with new key
4. Delete old key from Google Cloud Console
5. Close GitHub alert

**Option C: Clean Git History** (Not Recommended)
- Requires force push
- All collaborators must re-clone
- Very disruptive
- See IMPLEMENTATION_NOTES.md for details
- Only if you absolutely must

## Testing Your Setup

### Test 1: Map Loads
- Open the app
- You should see the map with markers
- If you see an error:
  - Check `config.js` exists
  - Check API key is correct
  - Check browser console for details

### Test 2: Click Challenge List Item
1. Go to Challenge List tab
2. Click on "Spaceship Earth Arrival Photo" (or any challenge)
3. Should switch to map and show that location
4. Info window should open
5. Try checking the box from there

### Test 3: Click Bouncing Marker
1. Go to Map tab
2. Find the orange bouncing marker (next challenge)
3. Click it
4. Info window should appear with challenge details

### Test 4: Check from Both Places
1. Check a box in the Challenge List
2. Go to Map - marker should be green/completed
3. Uncheck from the map info window
4. Go to List - should show as unchecked

## Need Help?

Read the detailed documentation:
- **SUMMARY.md** - Complete overview of all changes
- **IMPLEMENTATION_NOTES.md** - Detailed FAQ and troubleshooting
- **SECURITY.md** - API key security best practices
- **README.md** - Project overview and setup

## Quick Reference

| File | Purpose | Commit? |
|------|---------|---------|
| `config.js` | Your actual API key | ❌ NO (gitignored) |
| `config.example.js` | Template for others | ✅ YES |
| `index.html` | Main application | ✅ YES |

## Common Issues

### "Failed to load Google Maps"
- **Problem**: config.js missing or invalid
- **Solution**: Copy config.example.js to config.js and add your key

### "Map is all grey"
- **Problem**: Invalid API key or restrictions too tight
- **Solution**: Check key is correct and restrictions allow your domain

### "Clicking challenge does nothing"
- **Problem**: JavaScript error
- **Solution**: Check browser console for errors, refresh page

### GitHub still alerts
- **Problem**: Key in git history
- **Solution**: This is normal! Mark as false positive if restrictions are set

## Success Criteria

You know everything is working when:
- ✅ Map loads with colored markers
- ✅ Can click challenge items to navigate to map
- ✅ Can click markers to see info windows
- ✅ Can check/uncheck from both list and map
- ✅ Bouncing marker is clickable
- ✅ API key restrictions are verified in Google Cloud
- ✅ GitHub alert is handled appropriately

---

**Questions?** See IMPLEMENTATION_NOTES.md or open an issue!
