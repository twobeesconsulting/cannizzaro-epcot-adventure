# Config File Setup - Quick Answer

## The Question: "Do I save the config file locally or on GitHub?"

**Short Answer**: You need **BOTH files**, but in different places:

| File | Where? | Contains | Commit to GitHub? |
|------|--------|----------|-------------------|
| `config.js` | **LOCAL only** | Your actual API key | ❌ NO (gitignored) |
| `config.example.js` | **GitHub** | Template/placeholder | ✅ YES (already there) |

## Step-by-Step Setup

### For You (Repository Owner/User)

1. **Copy the example file**:
   ```bash
   cp config.example.js config.js
   ```

2. **Edit config.js** and add your real API key:
   ```javascript
   const CONFIG = {
       GOOGLE_MAPS_API_KEY: 'AIzaSy...'  // Your actual key
   };
   ```

3. **NEVER commit config.js** - it's already in `.gitignore` so Git will ignore it automatically

4. **Keep config.example.js on GitHub** - it's already there as a template for others

### For Contributors/Other Users

1. They see `config.example.js` on GitHub
2. They copy it: `cp config.example.js config.js`
3. They add their own API key to `config.js`
4. Their `config.js` stays local (not committed)

## Why This Way?

### 🔒 Security
- Your actual API key never goes to GitHub
- Each person uses their own key
- If repository is leaked, keys aren't exposed

### 👥 Collaboration
- `config.example.js` shows everyone what's needed
- New contributors know exactly what to set up
- No secrets shared in code

### ✅ Best Practice
- Industry standard approach
- Same pattern as `.env` / `.env.example`
- Used by thousands of projects

## Visual Guide

```
Your Computer                     GitHub Repository
├── config.js                     ├── config.example.js  ✅
│   (YOUR key)                    │   (template)
│   🔒 PRIVATE                    │   👥 PUBLIC
│   ❌ Don't commit              │   ✅ Already committed
│                                 │
├── config.example.js             ├── index.html
│   (template)                    ├── README.md
│   📋 Copy this                  └── ...
```

## Check Your Setup

### Verify config.js is gitignored:
```bash
git check-ignore config.js
```
Should output: `.gitignore:5:config.js	config.js`

### Verify config.js is NOT tracked:
```bash
git ls-files | grep config
```
Should output ONLY: `config.example.js` (not config.js)

### Verify you have both files locally:
```bash
ls -la config*.js
```
Should show both files exist on your computer

## Common Mistakes to Avoid

❌ **Don't** commit `config.js` with your real key  
❌ **Don't** put your key in `config.example.js`  
❌ **Don't** remove `config.example.js` from GitHub  
❌ **Don't** try to commit `config.js` (Git will ignore it anyway)  

✅ **Do** keep `config.js` local with your real key  
✅ **Do** keep `config.example.js` on GitHub as a template  
✅ **Do** make sure `config.js` is in `.gitignore`  
✅ **Do** share `config.example.js` with contributors  

## If You Accidentally Committed config.js

If you accidentally committed `config.js` with your real key:

1. **Immediately rotate your API key** in Google Cloud Console
2. Remove from git: `git rm --cached config.js`
3. Commit the removal: `git commit -m "Remove config.js from tracking"`
4. Generate a new key with proper restrictions
5. Add new key to your local `config.js`

## Questions?

- "Can I just hardcode my key?" → No, it would be in git history
- "Do teammates need their own keys?" → Yes, or they can share yours if properly restricted
- "What if config.js is missing?" → The app shows an error telling you to copy config.example.js
- "Is config.example.js sensitive?" → No, it only has placeholder text

---

**TL;DR**: `config.js` = local only (your key). `config.example.js` = GitHub (template). Both needed, different purposes.
