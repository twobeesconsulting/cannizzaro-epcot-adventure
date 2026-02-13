# Config Files - Visual Guide

## The Simple Answer

```
┌─────────────────────────────────────────────────────────────┐
│                                                               │
│  Question: Do I save config file locally or on GitHub?       │
│                                                               │
│  Answer: BOTH! But they are DIFFERENT files:                 │
│                                                               │
│  📁 config.js          → 🏠 LOCAL (your key)                 │
│  📁 config.example.js  → 🌐 GITHUB (template)                │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## File Comparison

```
┌──────────────────────────┬──────────────────────────┐
│      config.js           │   config.example.js      │
├──────────────────────────┼──────────────────────────┤
│ 🏠 Your computer ONLY    │ 🌐 GitHub repository     │
│ 🔒 Contains REAL key     │ 📋 Contains placeholder  │
│ ❌ Never commit          │ ✅ Already committed     │
│ 🔧 You create this       │ 📦 Comes with repo       │
│ ⚙️  Gitignored           │ 📤 Shared with everyone  │
└──────────────────────────┴──────────────────────────┘
```

## Setup Flow

```
Step 1: Clone Repository
┌────────────────────────────────────┐
│  GitHub Repository                 │
│  ✅ config.example.js (template)   │
│  ✅ index.html                     │
│  ✅ .gitignore                     │
└────────────────────────────────────┘
         │
         │ git clone
         ↓
┌────────────────────────────────────┐
│  Your Computer                     │
│  ✅ config.example.js (from repo)  │
│  ❌ config.js (doesn't exist yet)  │
└────────────────────────────────────┘


Step 2: Copy Template
         │
         │ cp config.example.js config.js
         ↓
┌────────────────────────────────────┐
│  Your Computer                     │
│  ✅ config.example.js              │
│  ✅ config.js (new copy!)          │
└────────────────────────────────────┘


Step 3: Add Your Key
         │
         │ Edit config.js
         ↓
┌────────────────────────────────────┐
│  Your Computer                     │
│  📋 config.example.js              │
│     GOOGLE_MAPS_API_KEY:           │
│     'YOUR_API_KEY_HERE'            │
│                                    │
│  🔒 config.js                      │
│     GOOGLE_MAPS_API_KEY:           │
│     'AIzaSyBc...real key'          │
└────────────────────────────────────┘


Step 4: Both Files Stay Different
┌─────────────────────┬──────────────────────┐
│  Your Computer      │  GitHub              │
├─────────────────────┼──────────────────────┤
│  config.example.js  │  config.example.js   │
│  (unchanged)        │  (unchanged)         │
│                     │                      │
│  config.js          │  (not on GitHub)     │
│  (real key)         │  (gitignored)        │
│  🔒 PRIVATE         │                      │
└─────────────────────┴──────────────────────┘
```

## What Git Sees

```bash
$ git status

On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	
  # config.js is NOT listed here!
  # Git ignores it because of .gitignore

nothing to commit, working tree clean
```

```bash
$ git check-ignore config.js
.gitignore:5:config.js	config.js
                        ↑
                This means Git is ignoring it ✅
```

## For Teams

```
Team Member A                Team Member B
──────────────              ──────────────

1. Clone repo               1. Clone repo
2. cp config.example.js     2. cp config.example.js
   → config.js                 → config.js
3. Add THEIR key            3. Add THEIR key
   (AIzaSyA...)                (AIzaSyB...)

Local: config.js            Local: config.js
GitHub: config.example.js   GitHub: config.example.js
         ↑
         Same template for everyone!
```

## Common Scenarios

### ✅ Correct: First Time Setup
```
$ ls config*
config.example.js  ← Came with repo

$ cp config.example.js config.js
$ vi config.js  ← Add real key

$ ls config*
config.example.js  ← Keep on GitHub
config.js          ← Keep local only
```

### ❌ Wrong: Trying to Commit config.js
```
$ git add config.js
# Nothing happens - Git ignores it!

$ git status
# config.js not shown - it's gitignored ✅
```

### ✅ Correct: Sharing with Team
```
# They clone repo
$ git clone https://github.com/you/repo
$ cd repo
$ ls config*
config.example.js  ← They see the template

# They create their own config.js
$ cp config.example.js config.js
$ vi config.js  ← They add their key
```

## File Contents Comparison

### config.example.js (on GitHub)
```javascript
// Configuration file for API keys
// Copy this file to config.js and add your key

const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'YOUR_API_KEY_HERE'
    //                    ↑
    //              Placeholder only!
};
```

### config.js (on your computer)
```javascript
// Configuration file for API keys
// Copy this file to config.js and add your key

const CONFIG = {
    GOOGLE_MAPS_API_KEY: 'AIzaSyBcgyqnX0qKID5n3dWgmX-AnHevToI6LSc'
    //                    ↑
    //              Your real key!
    //              Keep this private!
};
```

## Quick Reference Card

```
╔══════════════════════════════════════════════════════════╗
║  FILE               LOCATION      COMMIT?   CONTAINS     ║
╠══════════════════════════════════════════════════════════╣
║  config.js          Local         ❌ NO    Real API key  ║
║  config.example.js  GitHub        ✅ YES   Placeholder   ║
╚══════════════════════════════════════════════════════════╝

Remember: config.js = your secret, config.example.js = shared template
```

## Troubleshooting

### "Should I commit config.js?"
**No!** It's automatically ignored by Git. Keep it local.

### "What if config.example.js has my real key?"
**Don't do that!** Only put placeholder text in config.example.js.

### "My teammate needs the key. Do I commit config.js?"
**No!** They create their own config.js and add their own key.

### "Can multiple people use the same key?"
**Yes**, if the key has proper restrictions. But each person still creates their own local config.js file.

### "I accidentally committed config.js. What now?"
1. Remove it: `git rm --cached config.js`
2. Commit: `git commit -m "Remove config.js"`
3. Rotate your API key in Google Cloud Console
4. Add new key to your local config.js

---

**Bottom Line**: 
- `config.js` stays on **your computer** with **your key**
- `config.example.js` stays on **GitHub** as a **template**
- Both are needed, but serve different purposes!
