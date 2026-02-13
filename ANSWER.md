# ANSWER: Config File - Local or GitHub?

## Quick Answer

**You need BOTH files, but they go in DIFFERENT places:**

```
┌────────────────────────────────────────────────────────┐
│                                                        │
│  config.js          → 🏠 YOUR COMPUTER (private)       │
│  config.example.js  → 🌐 GITHUB (shared template)     │
│                                                        │
└────────────────────────────────────────────────────────┘
```

## What You Do

### Step 1: Copy the template (one time)
```bash
cp config.example.js config.js
```

### Step 2: Add YOUR key to config.js
```javascript
// config.js (stays on your computer)
const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'AIzaSy...your-actual-key'
};
```

### Step 3: That's it!
- `config.js` stays LOCAL (Git ignores it automatically)
- `config.example.js` stays on GitHub (already there)

## Why Two Files?

| Purpose | File | Location |
|---------|------|----------|
| Your actual key (secret) | `config.js` | Your computer only |
| Template for others | `config.example.js` | GitHub |

## Will Git Commit My Key?

**No!** The file `config.js` is in `.gitignore`, so Git automatically ignores it.

Try it:
```bash
$ git status
# config.js won't appear - Git ignores it!

$ git check-ignore config.js
.gitignore:5:config.js	config.js
                        ↑ This means it's ignored ✅
```

## For More Details

- **Quick overview**: [CONFIG_FAQ.md](CONFIG_FAQ.md)
- **Visual diagrams**: [CONFIG_VISUAL_GUIDE.md](CONFIG_VISUAL_GUIDE.md)
- **Setup guide**: [QUICKSTART.md](QUICKSTART.md)

## One-Sentence Summary

**`config.js` stays on your computer with your real key, while `config.example.js` stays on GitHub as a template for everyone else.**
