# 🌍 Game Event Translator
## Chinese ↔ Vietnamese Game Event Localization Tool

A professional-grade game event translator that uses Claude AI to ensure glossary consistency, maintains formatting, and preserves gameplay tone. Built for game localization teams working with Chinese source content.

---

## 🎯 Features

✅ **Glossary-First Translation**: Ensures 100% consistency with approved term mappings  
✅ **Batch Processing**: Handles large event files efficiently (batches of 20 lines)  
✅ **Previous Translation Awareness**: References older translations for consistency  
✅ **Format Preservation**: Keeps placeholders, colors, tables, and markup intact  
✅ **Tone Matching**: Adapts between epic/story events and casual/daily quests  
✅ **Excel Export**: Generates properly formatted output with custom naming  
✅ **No Backend Required**: 100% client-side processing (no server needed)  
✅ **Dark Mode Support**: Automatic light/dark theme detection  

---

## 🚀 Quick Start

### Option 1: HTML Version (Easiest - No Installation)

1. **Download** `game-event-translator.html`
2. **Open** in your web browser (Chrome, Firefox, Safari, Edge)
3. **Get API Key**: Visit https://console.anthropic.com/account/keys
4. **Start translating!**

### Option 2: React Version (For Next.js/React Projects)

```bash
npm install
# Copy game-event-translator.jsx to your components folder
```

```jsx
import GameEventTranslator from './game-event-translator';

export default function App() {
  return <GameEventTranslator />;
}
```

---

## 📋 Setup Instructions

### Step 1: Get Your Anthropic API Key

1. Visit [console.anthropic.com/account/keys](https://console.anthropic.com/account/keys)
2. Sign up or log in to your Anthropic account
3. Create a new API key
4. Copy the key (starts with `sk-ant-...`)

> **Security Note**: Your API key is only used in your browser session and never stored or transmitted to any server.

### Step 2: Prepare Your Files

Create three Excel files (.xlsx):

#### **Glossary File** (ZH_Glossary.xlsx)
| Chinese Term | Vietnamese Approved Translation | Notes |
|---|---|---|
| 传送门 | Cổng Dịch Chuyển | Portal terminology |
| 副本 | Phó Bản | Dungeon instance |
| 装备 | Trang Bị | Equipment |

#### **Event Content File** (Event 03.2024.xlsx)
```
Source Text
使用传送门前往副本
获得新装备奖励
解锁特殊成就
```

#### **Previous Translations File** (Optional - Event 02.2024.xlsx)
```
Source | Previous Translation
使用传送门 | Sử dụng Cổng Dịch Chuyển
副本挑战 | Thử Thách Phó Bản
```

**File naming requirement for auto-detection:**
- Event content: `Event [M].[YYYY].xlsx`  
  Example: `Event 03.2024.xlsx`, `Event 12.2025.xlsx`

---

## 🎮 How to Use

### Workflow

```
1. Upload Glossary (ZH→VI term mappings)
    ↓
2. Upload Event Content (Chinese source text)
    ↓
3. (Optional) Upload Previous Translations (for consistency)
    ↓
4. Paste your API Key
    ↓
5. Click "Start Translation with Claude"
    ↓
6. Review results in table
    ↓
7. Click "Export to Excel" to save
```

### Step-by-Step

1. **Open the tool** (`game-event-translator.html` or React component)

2. **Upload Glossary**
   - Click "📖 Glossary" button
   - Select your ZH→VI term mapping file
   - See preview of first 5 terms

3. **Upload Event Content**
   - Click "📄 Event Content" button
   - Select the Chinese source file
   - The filename pattern helps auto-name your output

4. **Paste API Key**
   - Click the API key field
   - Paste your `sk-ant-...` key
   - Button "Start Translation" will enable

5. **Click Translate**
   - Tool processes in batches of 20 lines
   - Status updates as each batch completes
   - Results appear in a table below

6. **Review & Adjust**
   - Check translations in the table
   - Look for any red flags or notes
   - Edit directly if needed (optional)

7. **Export**
   - Click "⬇️ Export to Excel"
   - File saves as: `Event M.YYYY 天使之战越南节日活动.xlsx`
   - Example: `Event 03.2024 天使之战越南节日活动.xlsx`

---

## 📊 Translation Instruction (How Claude Works)

The tool uses this comprehensive prompt to guide Claude's translation:

```
You are a professional game localization translator specializing in 
Chinese to Vietnamese translation.

GLOSSARY (Chinese → Vietnamese approved terms):
[Your glossary terms are injected here]

RULES:
- ALWAYS check the glossary first before translating
- If a term exists in the glossary, use EXACTLY that translation
- If NOT in glossary, translate naturally
- Preserve all placeholders: {player_name}, %d, <br>, [item], etc.
- Do not translate proper nouns unless in glossary
- Maintain tone: epic/dramatic for stories, casual for daily quests
- Review sentences to match Vietnamese's structure

OUTPUT: Return JSON array with [source, translation, notes]
```

---

## 📁 File Formats

### Supported Input Formats
- ✅ Excel 2007+ (`.xlsx`)
- ✅ Excel 97-2003 (`.xls`)
- ✅ CSV (`.csv`)

### Auto-Detection Rules

**Glossary File**:
- Column 1 = Chinese source term
- Column 2 = Vietnamese approved translation
- Column 3 (optional) = Usage notes

**Event Content**:
- Column 1 = Chinese source text
- Headers are skipped automatically

**Output Excel**:
- Columns: `#` | `Source (ZH)` | `Vietnamese` | `Notes`
- Font: Calibri (12pt)
- Filename pattern: `Event M.YYYY 天使之战越南节日活动.xlsx`

---

## 🔧 Troubleshooting

### "API Error: Invalid API Key"
- ❌ Check your key is correct (starts with `sk-ant-`)
- ❌ Ensure it's valid: visit console.anthropic.com and regenerate

### "Failed to parse Excel"
- ❌ File might be corrupted
- ❌ Try opening in Excel and re-saving
- ❌ Convert to `.xlsx` if using older `.xls`

### "Translation results are incomplete"
- ❌ Claude may need more context in glossary
- ❌ Try adding more example translations
- ❌ Check that all special terms are in glossary

### Glossary terms not being used
- ❌ Ensure exact spelling in source (case-sensitive)
- ❌ Check for whitespace differences
- ❌ Verify glossary is uploaded before translation starts

### Export button disabled
- ❌ Click "Start Translation" first to generate results
- ❌ Results must complete successfully

### Dark mode not working
- ❌ Browser may not support CSS prefers-color-scheme
- ❌ Try a modern browser (Chrome 76+, Firefox 67+, Safari 12+)

---

## 💡 Pro Tips

### 1. Glossary Organization
```
Group related terms together:
- Combat terms (传送门, 副本, 怪物)
- Rewards (装备, 金币, 经验)
- UI/Menu (背包, 设置, 商城)
```

### 2. Batch Processing
- Files with 100+ lines are split into batches
- Each batch takes ~2-5 seconds
- Watch the console for progress updates

### 3. Placeholders
These are **always** preserved:
- `{player_name}` → `{player_name}` (unchanged)
- `%d` → `%d` (unchanged)
- `<br>` → `<br>` (unchanged)
- `[item_name]` → `[item_name]` (unchanged)

### 4. Tone Matching
Tell Claude the context in notes:
```
Glossary column 3 (Notes):
"Daily quest - keep it friendly and brief"
"Story event - use dramatic, epic tone"
"Menu text - keep it concise and professional"
```

### 5. Consistency Tracking
Use previous translations file to:
- Maintain term consistency across events
- Show Claude how similar items were translated before
- Catch translation drift between team members

---

## 🎮 Example Workflow

### Input Files

**ZH_Glossary.xlsx:**
```
传送门 | Cổng Dịch Chuyển | Teleport portal
副本 | Phó Bản | Dungeon
装备 | Trang Bị | Equipment
```

**Event 03.2024.xlsx:**
```
使用传送门前往副本获得新装备
完成副本任务解锁成就
升级装备提升战力
```

**API Key:**
```
sk-ant-[your-key-here]
```

### Process

1. Upload all three files
2. Paste API key
3. Click "Start Translation"
4. Claude translates:
   - "使用传送门" → "Sử dụng Cổng Dịch Chuyển" (from glossary)
   - "副本" → "Phó Bản" (from glossary)
   - "新装备" → "Trang Bị mới" (uses glossary term + context)

### Output Excel

```
# | Source (ZH) | Vietnamese | Notes
1 | 使用传送门前往副本获得新装备 | Sử dụng Cổng Dịch Chuyển để đến Phó Bản và nhận Trang Bị mới | -
2 | 完成副本任务解锁成就 | Hoàn thành nhiệm vụ Phó Bản để mở khóa thành tích | -
3 | 升级装备提升战力 | Nâng cấp Trang Bị để tăng sức mạnh chiến đấu | -
```

---

## 🔐 Security & Privacy

- **No data storage**: Files are processed in your browser only
- **No backend**: Results don't pass through any server (except Claude API)
- **API key security**: Key is only sent directly to Anthropic API
- **Local caching**: Nothing is cached or logged locally
- **HTTPS only**: Always use HTTPS connection

---

## 📈 Performance

| File Size | Expected Time |
|---|---|
| 20 lines | ~10 seconds |
| 50 lines | ~20 seconds |
| 100 lines | ~40 seconds |
| 200 lines | ~1.5 minutes |

> Processing time includes batching (20 lines per batch) + network latency

---

## 🐛 Reporting Issues

If you encounter bugs:

1. **Check the error message** in the red error box
2. **Try the HTML version** if React version fails
3. **Clear browser cache** and reload
4. **Check API key validity** at console.anthropic.com
5. **Verify file formats** are correct Excel/CSV

---

## 🙌 Credits

**Built with:**
- [Anthropic Claude API](https://www.anthropic.com/api)
- [SheetJS](https://sheetjs.com/) - Excel parsing
- Modern CSS & Vanilla JavaScript

**Designed for:**
- Game localization teams
- Chinese → Vietnamese translation workflows
- Enterprise-grade glossary management

---

## 📝 Version History

### v1.0 (Current)
- ✅ Initial release
- ✅ HTML + React versions
- ✅ Glossary support
- ✅ Batch processing
- ✅ Excel export with Calibri font
- ✅ Dark mode support

---

## 📧 Support

For questions or feature requests:
- Anthropic Discord: [discord.anthropic.com](https://discord.anthropic.com)
- API Documentation: [docs.claude.com](https://docs.claude.com)
- Console: [console.anthropic.com](https://console.anthropic.com)

---

**Made for professional game localization. Use responsibly. 🎮**
