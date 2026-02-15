# 🎉 Vincent's 21st Birthday EPCOT Adventure

An interactive web application created for Vincent's epic 21st birthday celebration at EPCOT! This app helps track the "Drinking Around the World" challenge and provides an engaging way to experience the Cannizzaro family's magical adventure.

Follow the journey: **[@magicaldocsarahadventures](https://instagram.com/magicaldocsarahadventures)** on Instagram!

## 🎂 About This Adventure

This app was created for **Vincent's 21st Birthday Celebration** on **March 8, 2026** at EPCOT with the **Cannizzaro Family**. It's designed to make the "Drinking Around the World" challenge memorable and fun by providing interactive tracking and celebration features.

Share your adventures with **@magicaldocsarahadventures**!

## ✨ Features

- **Interactive Map**: Navigate through EPCOT with an interactive Google Maps view showing all challenge locations
- **Challenge Tracking**: Click on challenges to mark them as completed and track your progress
- **Progress Dashboard**: Real-time progress bar and statistics showing completed challenges, countries visited, and photo opportunities
- **Celebration Modal**: Special animations and celebrations when completing challenges and finishing the entire journey
- **Mobile-Friendly**: Fully responsive design optimized for use on mobile devices during your EPCOT visit
- **Click Navigation**: Click any challenge in the list to automatically navigate to its location on the map
- **Reset Progress**: Easily reset all progress to experience the celebration multiple times

## 🚀 How to Use

1. **View Challenges**: Open the app and switch between the Interactive Map and Challenge List tabs
2. **Navigate**: Click on any challenge card to see its location on the map
3. **Complete Challenges**: As you complete each challenge at EPCOT, click the checkbox to mark it done
4. **Track Progress**: Watch your progress bar fill up and see your stats grow
5. **Celebrate**: Enjoy special celebration animations when completing challenges
6. **Reset**: Use the "Reset Progress" button to start the adventure again

Don't forget to tag **@magicaldocsarahadventures** when sharing your EPCOT adventure!

## 📱 Mobile Experience

This app is optimized for mobile use! Simply:
- Open `index.html` on your phone
- Add to home screen for quick access
- Use it while exploring EPCOT
- All features work seamlessly on mobile devices

## 🛠️ Setup Instructions

### Quick Start (No Setup Required)

Simply open `index.html` in your web browser - that's it! The app works immediately.

**Note**: The map feature requires a Google Maps API key. If you want to use the interactive map:

1. Copy `config.example.js` to `config.js`:
   ```bash
   cp config.example.js config.js
   ```

2. Add your Google Maps API key to `config.js`:
   ```javascript
   const CONFIG = {
       GOOGLE_MAPS_API_KEY: 'YOUR_API_KEY_HERE'
   };
   ```

3. Refresh the page

**Important**: The `config.js` file is gitignored for security. Each user needs their own API key.

### Getting a Google Maps API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable "Maps JavaScript API" and "Places API"
4. Create credentials (API Key)
5. **Restrict your API key** to prevent unauthorized use:
   - Set HTTP referrer restrictions
   - Limit to Maps JavaScript API and Places API only

For detailed security information, see [SECURITY.md](SECURITY.md).

## 📁 Project Structure

```
├── index.html          # Main application file (all-in-one)
├── config.example.js   # Template for API configuration
├── config.js          # Your local API key (gitignored)
└── README.md          # This file
```

## 🎨 Credits

**Created for Vincent's 21st Birthday Adventure** 🎂

Made with ❤️ for the **Cannizzaro Family** EPCOT trip on March 8, 2026

Follow more magical adventures: **[@magicaldocsarahadventures](https://instagram.com/magicaldocsarahadventures)**

---

## 📖 Additional Documentation

- [QUICKSTART.md](QUICKSTART.md) - Quick start guide for users
- [CONFIG_FAQ.md](CONFIG_FAQ.md) - Frequently asked questions about configuration
- [SECURITY.md](SECURITY.md) - Security best practices for API keys
- [GOOGLE_MAPS_API_LINK.md](GOOGLE_MAPS_API_LINK.md) - Complete Google Maps setup instructions

## 🎉 Have a Magical Adventure!

Enjoy your 21st birthday, Vincent! May your journey around the world at EPCOT be filled with amazing memories, great drinks, and lots of laughter! 🌍🍻✨

Remember to tag **@magicaldocsarahadventures** in all your posts!
