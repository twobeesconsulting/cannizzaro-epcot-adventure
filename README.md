# cannizzaro-epcot-adventure
Vincent's Epic EPCOT Adventure

## 🗺️ Need the Google Maps API Link?

**See [GOOGLE_MAPS_API_LINK.md](GOOGLE_MAPS_API_LINK.md) for the API URL and complete setup instructions!**

The Google Maps API link is: `https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY_HERE&libraries=places`

## Setup Instructions

1. Clone the repository
2. **Copy `config.example.js` to `config.js`** (stays local, not committed)
   ```bash
   cp config.example.js config.js
   ```
3. **Add your Google Maps API key to `config.js`** (your actual key, keep it local)
4. Open `index.html` in your browser or serve it via a local web server

**Important**: 
- ✅ `config.js` = **Local only** (contains your real key, gitignored)
- ✅ `config.example.js` = **On GitHub** (template, already committed)
- See [CONFIG_FAQ.md](CONFIG_FAQ.md) for detailed explanation

## Google Maps API Key Setup

**📖 For complete details on the API link and setup, see [GOOGLE_MAPS_API_LINK.md](GOOGLE_MAPS_API_LINK.md)**

This application requires a Google Maps API key. **Important security note**: Since this is a frontend-only application, the API key will be visible in the browser. To protect your API key:

1. **Create a restricted API key** in Google Cloud Console
2. **Apply the following restrictions**:
   - **Application restrictions**: HTTP referrers (set to your domain)
   - **API restrictions**: Restrict to "Maps JavaScript API" and "Places API" only
3. **Set usage limits** to prevent unexpected charges
4. **Monitor usage** regularly in Google Cloud Console

Even with a restricted key, GitHub's secret scanning may still alert you. This is expected behavior for frontend applications. The key restrictions on Google's end provide the actual security.

For more details, see [SECURITY.md](SECURITY.md).
