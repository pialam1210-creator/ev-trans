# Game Event Translator - GitHub Setup & Deployment

## 🚀 Quick Deploy (30 seconds)

### Option 1: GitHub Pages (Easiest)

```bash
# 1. Fork or clone this repo
git clone https://github.com/YOUR_USERNAME/game-event-translator.git
cd game-event-translator

# 2. Go to Settings → Pages → Source → main branch
# (GitHub will automatically serve the HTML file)

# 3. Your translator is live at:
# https://YOUR_USERNAME.github.io/game-event-translator/
```

### Option 2: Deploy to Vercel (1 click)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new?utm_medium=default-template&filter=next.js)

1. Click the "Deploy with Vercel" button
2. Connect your GitHub account
3. Select this repository
4. Vercel automatically deploys

Your app is live in ~1 minute at `https://[your-project].vercel.app/`

### Option 3: Netlify (Drag & Drop)

1. Visit [netlify.com/drop](https://netlify.com/drop)
2. Drag & drop `game-event-translator.html`
3. Your app is live instantly with a Netlify URL

---

## 📦 File Structure

```
game-event-translator/
├── game-event-translator.html    ← Main tool (open in browser)
├── game-event-translator.jsx     ← React component
├── README.md                      ← Full documentation
├── example-glossary.xlsx          ← Sample glossary
├── example-event.xlsx             ← Sample event content
└── GITHUB-SETUP.md               ← This file
```

---

## 🎯 First Time Setup

### 1. Get Your API Key

Visit: https://console.anthropic.com/account/keys

- Sign up (free)
- Create API key
- Copy the `sk-ant-...` key

### 2. Open the Tool

**HTML Version** (Recommended):
- Download `game-event-translator.html`
- Double-click to open in browser
- Paste API key when prompted

**React Version**:
```bash
npm install
npm run dev  # Your tool runs at localhost:3000
```

### 3. Test with Sample Files

We include example files:
- `example-glossary.xlsx` - Sample ZH→VI terms
- `example-event.xlsx` - Sample Chinese event text

Upload these to test without preparing real files!

---

## 🔧 Configuration

### Environment Variables (React Version Only)

Create `.env.local`:
```
REACT_APP_API_ENDPOINT=https://api.anthropic.com/v1/messages
REACT_APP_MODEL=claude-sonnet-4-20250514
```

### Customization

**Change the system prompt** (in the code):

```javascript
const buildInstructionPrompt = () => {
  return `You are a professional game localization translator...
  [Customize this section]
  `;
};
```

**Change export filename pattern**:

```javascript
const fileName = `Event ${month}.${year} YOUR_GAME_NAME.xlsx`;
```

**Change supported file formats**:

```html
<!-- In HTML -->
<input accept=".xlsx,.xls,.csv,.tsv" />

<!-- Or restrict to .xlsx only -->
<input accept=".xlsx" />
```

---

## 🌐 Deployment Checklist

- [ ] API key is removed from code
- [ ] `game-event-translator.html` is in root directory
- [ ] GitHub Pages / Netlify / Vercel is configured
- [ ] URL is accessible from public internet
- [ ] Test with example files works
- [ ] Error messages display correctly
- [ ] Export button creates correct filename

---

## 🐛 Troubleshooting Deployment

### GitHub Pages

**Issue**: 404 error when visiting page

**Solution**:
1. Go to Settings → Pages
2. Source should be "Deploy from branch" → "main"
3. Wait 2-3 minutes for GitHub to build
4. Check the URL format: `https://USERNAME.github.io/REPO/`

### Vercel

**Issue**: CORS error on file upload

**Solution**:
- This is NOT a CORS issue - Vercel serves HTML fine
- Check your browser console for actual error
- Clear browser cache: Ctrl+Shift+Delete

### Netlify

**Issue**: CSS/fonts not loading

**Solution**:
- Netlify automatically handles this
- Try refreshing the page (hard refresh: Ctrl+F5)
- Check browser DevTools → Network tab

---

## 📊 Analytics (Optional)

Add Google Analytics to track usage:

```html
<!-- Add this before </body> -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_ID');
</script>
```

---

## 🔒 Security Best Practices

✅ **DO:**
- Use HTTPS only (GitHub Pages / Vercel / Netlify default to this)
- Generate new API key for each team member
- Rotate API keys monthly
- Monitor API usage at console.anthropic.com

❌ **DON'T:**
- Store API keys in code or version control
- Share API keys in Slack/Email
- Use the same API key across multiple projects
- Commit `.env` files with secrets

### Git Security

If you accidentally commit an API key:

```bash
# Remove from git history (careful!)
git filter-branch --tree-filter 'rm -f filename' HEAD

# Or use git-secrets
npm install -g git-secrets
git secrets --install
```

---

## 📈 Performance Optimization

### HTML Version

Current load time: **~2KB (gzipped)**

To further optimize:
```html
<!-- Lazy load SheetJS only when needed -->
<script type="module">
  document.getElementById('glossaryFile').addEventListener('change', async () => {
    if (!window.XLSX) {
      const script = document.createElement('script');
      script.src = 'https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.min.js';
      document.body.appendChild(script);
    }
  });
</script>
```

### React Version

Build optimization:
```bash
npm run build
# Output: ~45KB (includes all dependencies)
# With compression: ~12KB gzipped
```

---

## 🤝 Contributing

We welcome improvements!

```bash
# 1. Fork the repo
# 2. Create a feature branch
git checkout -b feature/your-feature

# 3. Make changes
# 4. Test thoroughly
# 5. Commit and push
git push origin feature/your-feature

# 6. Create a Pull Request
```

---

## 📝 License

MIT License - Free to use, modify, and distribute

---

## 🎮 Use Cases

This tool is perfect for:

- **Game Localization Teams**: Translate event content with glossary enforcement
- **Indie Games**: Chinese → Vietnamese localization on a budget
- **Community Translations**: Fan-translated game content
- **Professional Studios**: Enterprise-grade glossary management
- **Learning**: Example of Claude API integration + React patterns

---

## 💬 FAQ

**Q: Can I use this for other language pairs?**

A: Yes! Modify the system prompt and glossary format to support:
- Chinese → Spanish
- Chinese → French  
- Chinese → Portuguese
- Any language pair Claude supports

**Q: Can I host this privately?**

A: Yes! Use the React version with your own Next.js/Vercel setup:
```bash
npx create-next-app --template with-react game-translator
# Copy game-event-translator.jsx into /app
```

**Q: What if I have 500+ lines to translate?**

A: The tool batches in groups of 20 automatically. Just:
1. Upload your file
2. Click translate
3. Let it process (check browser DevTools → Console for progress)
4. Batching is transparent - you see final results when done

**Q: Can I edit translations before export?**

A: Not yet - results are displayed as read-only. To edit:
1. Export the Excel file
2. Open in Excel/Sheets
3. Edit manually
4. Glossary ensures consistency, but you can tweak tone/phrasing

**Q: Does this work offline?**

A: No - it requires:
1. Internet connection
2. Valid Anthropic API key
3. Access to api.anthropic.com

**Q: How much does this cost?**

A: You only pay for Claude API usage:
- **$3 per 1M input tokens** (~1.3M Chinese characters)
- **$15 per 1M output tokens** (~650K characters)
- Typical translation batch (100 lines): ~$0.02-0.05 USD

**Q: Can I use my team's API key?**

A: Not recommended - rotate keys monthly and use individual keys.
- Create separate keys in console.anthropic.com for each team member
- This lets you track who used what
- Easier to revoke if someone leaves

---

## 🆘 Getting Help

### Documentation
- Full guide: Read `README.md`
- API docs: https://docs.claude.com
- Anthropic Discord: https://discord.anthropic.com

### Common Issues

1. **"Invalid API Key"** → Check console.anthropic.com
2. **"CORS error"** → Use the HTML version (no build needed)
3. **"File won't upload"** → Ensure it's valid Excel format
4. **"Translation is wrong"** → Check your glossary is loaded correctly

### Report a Bug

1. Check console error (F12 → Console tab)
2. Note your browser version
3. Try the example files
4. Create an issue with error message

---

## 🚀 Next Steps

1. **Deploy today**: Pick GitHub Pages / Vercel / Netlify above
2. **Share your URL**: Let your team test it
3. **Customize**: Modify system prompt for your game
4. **Iterate**: Get feedback, refine translations
5. **Scale**: Add batch processing, team management, etc.

---

**Ready to go live? Start with the HTML version - no setup required! 🚀**

Open `game-event-translator.html` in your browser right now.
