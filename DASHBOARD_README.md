# 投資分析報告中心 - Dashboard Documentation

## Overview
Professional investment dashboard showcasing daily Top 10 stock picks with CFA-framework deep analysis reports. Built with responsive dark theme design, mobile-friendly, zero dependencies.

**File**: `index.html`  
**Size**: 33 KB  
**Platform**: GitHub Pages / Static Site

---

## Features

### 1. **Daily Top 10 Picks Section**
- Ranked stock cards (1-10) with gold rank badge
- Six-dimension score breakdown:
  - 基本面 (Fundamentals)
  - 籌碼面 (Chip/Supply)
  - 技術面 (Technical)
  - 消息面 (Catalysts)
  - 總經 (Macro)
  - 產業展望 (Industry Outlook)
- Visual progress bars for each score (0-10 scale)
- Current price, target price, upside % in real-time color coding
- Rating badges: 🟢 Buy / 🟡 Hold / 🔴 Sell
- Market flags: 🇹🇼 Taiwan / 🇺🇸 USA
- Links to deep research reports (if available)

### 2. **Calendar Navigation**
- Quick buttons: Today, Yesterday, This Week
- Date picker for custom date selection
- Current date display (localized to Taiwan timezone)
- Active state indicator on selected date

### 3. **Stats Bar**
- Total deep research reports count
- Average 6D score across all picks
- Taiwan stock market percentage distribution
- Buy-rated stocks ratio

### 4. **Deep Research Reports Grid**
- All 6 published deep analysis reports displayed
- Each card shows: Ticker, Name, Date, Rating
- Direct links to full HTML reports
- Buy/Hold/Sell color coding

### 5. **Archive Section**
- All historical reports indexed:
  - 1503.TW 士林電機 (Shihlin Electric)
  - 1504.TW 東元電機 (TECO)
  - 1513.TW 中興電工 (Chung-Hsin Electric)
  - 1514.TW 亞力電機 (Alex)
  - 2330.TW 台積電 (TSMC)
  - 2383.TW 台光電 (Elite Material)

### 6. **Responsive Design**
- Desktop: Multi-column grid layout
- Tablet (≤768px): 2-column cards
- Mobile (≤640px): Single column, optimized spacing
- Touch-friendly buttons (min 44px height)
- Readable typography (min 14px on mobile)
- Viewport meta tag for proper scaling

---

## How to Use

### Basic Navigation
1. **View Today's Picks**: Page loads with current date selected
2. **Change Date**: Click calendar buttons or use date picker
3. **View Deep Report**: Click "閱讀深度報告 →" link on any pick card
4. **Browse Archive**: Scroll to archive section for all historical reports

### Mobile Usage
- Swipe or tap to navigate
- Date picker works with native date input
- Cards stack vertically for easier reading
- All links are touch-optimized

### Integration with JSON Data
The dashboard is ready to load dynamic data from JSON files:

```javascript
// Expected JSON structure for daily picks
{
  "date": "2026-03-11",
  "picks": [
    {
      "rank": 1,
      "ticker": "2330.TW",
      "name": "台積電",
      "nameEn": "TSMC",
      "market": "TW",
      "price": 890,
      "currency": "TWD",
      "rating": "Buy",
      "target_price": 1050,
      "upside": "+18%",
      "scores": {
        "基本面": 9,
        "籌碼面": 8,
        "技術面": 7,
        "消息面": 8,
        "總經": 7,
        "產業展望": 9
      },
      "total_score": 48,
      "summary": "Brief investment thesis",
      "deep_report": "reports/deep/2330-2026-03-11.html"
    }
    // ... up to 10 picks
  ]
}
```

---

## Customization Guide

### Change Colors
Edit CSS variables in `<style>`:
```css
/* Dark blue theme (current) */
background: linear-gradient(135deg, #0f172a 0%, #1a202c 100%);

/* For light theme, change to */
background: #f8fafc;
color: #1e293b;
```

### Add New Reports
In `REPORT_ARCHIVE` array:
```javascript
{
  ticker: '9999.TW',
  name: 'Company Name',
  date: '2026-03-15',
  rating: 'Buy',
  file: '9999-2026-03-15.html'
}
```

### Modify Stock Data
In `SAMPLE_PICKS` object:
```javascript
'2026-03-15': [
  {
    rank: 1,
    ticker: 'xxxx.TW',
    // ... full pick object
  }
]
```

### Update Header
```html
<h1>Your Custom Title</h1>
<p>Your Custom Subtitle</p>
<div class="subtitle">Data Period: YYYY-MM</div>
```

---

## Technical Details

### Dependencies
- **Zero external dependencies** ✅
- Pure HTML5, CSS3, Vanilla JavaScript
- No CDN libraries (fonts/icons embedded via Unicode)
- Works completely offline

### Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari, Chrome Mobile)

### Performance
- Lightweight: 33 KB single file
- No render-blocking resources
- Fast animations (GPU-accelerated)
- Optimized for mobile (minimal layout shifts)

### Accessibility
- Semantic HTML structure
- Color contrast ratio ≥4.5:1 (WCAG AA)
- Keyboard navigable
- Touch target size ≥44x44px

---

## Deployment

### GitHub Pages
1. Place `index.html` in repo root or `/docs` folder
2. Enable GitHub Pages in repo settings
3. Access at: `https://username.github.io/investment-reports/`

### Local Server
```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server

# Then visit: http://localhost:8000
```

### Static Hosting
Works on any static file hosting (Netlify, Vercel, AWS S3, etc.)

---

## Data Updates

### To Add Daily Picks
Option 1: Manual edit of `SAMPLE_PICKS` object
Option 2: Implement API integration using fetch():
```javascript
const response = await fetch(`data/daily-picks-${dateStr}.json`);
const picks = await response.json();
renderPicks(picks.picks);
```

### To Refresh Archive
Keep `REPORT_ARCHIVE` array updated with new reports:
```javascript
REPORT_ARCHIVE.push({
  ticker: 'XXXX.TW',
  name: 'Company',
  date: '2026-03-15',
  rating: 'Buy',
  file: 'XXXX-2026-03-15.html'
});
```

---

## Score Interpretation

| Score Range | Assessment |
|-------------|-----------|
| 50-60 | 🟢 Strong Buy (All dimensions aligned) |
| 45-49 | 🟡 Moderate Buy (Most dimensions positive) |
| 40-44 | 🟡 Hold (Mixed signals) |
| 35-39 | 🔴 Weak Hold (Caution warranted) |
| <35 | 🔴 Sell (Avoid) |

---

## Rating Definitions

- **🟢 Buy**: Upside ≥15% with favorable fundamentals + technicals
- **🟡 Hold**: Fair value, wait for better entry or hold existing positions
- **🔴 Sell**: Overvalued or deteriorating fundamentals

---

## Footer & Disclaimers
- Required legal notice visible on all pages
- CFA Buy-Side Framework attribution
- Investment risk warning in place

---

## Support & Maintenance

### Common Issues

**Q: Charts not updating?**  
A: Check `SAMPLE_PICKS` object has data for selected date.

**Q: Links to reports broken?**  
A: Verify HTML files exist in same directory or update file paths.

**Q: Mobile layout looks wrong?**  
A: Clear browser cache (Ctrl+Shift+Del) and reload.

**Q: Date picker not working?**  
A: Ensure browser supports HTML5 date input (Chrome, Firefox, Safari all support).

---

**Last Updated**: 2026-03-11  
**Version**: 1.0  
**Author**: Investment Analysis Agent
