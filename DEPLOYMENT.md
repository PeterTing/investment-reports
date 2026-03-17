# GitHub Pages Deployment Guide

## Quick Start (2 minutes)

### Step 1: Enable GitHub Pages
1. Go to repo Settings → Pages
2. Select: Source = `Deploy from a branch`
3. Branch = `main`, Folder = `/ (root)` or `/docs`
4. Click Save

### Step 2: Verify
- Dashboard will be live at: `https://yourusername.github.io/investment-reports/`
- Takes 1-2 minutes to build

---

## File Structure for Deployment

```
investment-reports/
├── index.html                    ← Main dashboard (33 KB)
├── 1503-2026-03-11.html         ← Deep report
├── 1504-2026-03-06.html         ← Deep report
├── 1513-2026-03-11.html         ← Deep report
├── 1514-2026-03-09.html         ← Deep report
├── 2330-2026-03-06.html         ← Deep report
├── 2383-2026-03-06.html         ← Deep report
└── (optional) data/
    ├── daily-picks-2026-03-11.json
    ├── daily-picks-2026-03-10.json
    └── ...
```

---

## Features Working on GitHub Pages

✅ All interactive features work offline  
✅ Date picker for navigation  
✅ Calendar buttons (Today/Yesterday/Week)  
✅ All 6 reports linked and working  
✅ Archive section with quick links  
✅ Stats bar auto-calculating  
✅ Mobile responsive design  
✅ Dark theme optimized  

---

## Testing Before Deployment

### Local Test (Recommended)
```bash
cd /sessions/nice-eager-fermi/investment-reports

# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js
npx http-server

# Visit: http://localhost:8000
```

### What to Test
- [ ] Header displays correctly
- [ ] Stats bar shows: 6 reports, 48 score, 100% TW, 3/6 Buy
- [ ] Calendar buttons work (Today/Yesterday/Week)
- [ ] Date picker selects dates
- [ ] Top 10 picks display with scores
- [ ] Cards hover effect works
- [ ] "深度研究報告" section shows 6 cards
- [ ] Archive section shows all 6 reports
- [ ] All report links (blue arrows) point to correct HTML files
- [ ] Mobile responsive (open DevTools, toggle device toolbar)

---

## Customization Before Deploy

### 1. Update the Date
In `index.html`, find and update:
```html
<div class="subtitle">數據基期：2026/03 | CFA Buy-Side Framework</div>
```

### 2. Add Today's Picks (Optional)
In JavaScript `SAMPLE_PICKS` object:
```javascript
'2026-03-12': [
  {
    rank: 1,
    ticker: '2330.TW',
    name: '台積電',
    // ... full object ...
  }
]
```

### 3. Update Report Archive
If you have new reports, add to `REPORT_ARCHIVE`:
```javascript
{ ticker: '9999.TW', name: 'Company', date: '2026-03-12', rating: 'Buy', file: '9999-2026-03-12.html' }
```

---

## Advanced: JSON Data Integration

To load dynamic picks from JSON files:

### 1. Create data folder
```bash
mkdir -p investment-reports/data/
```

### 2. Create JSON file: `data/daily-picks-2026-03-12.json`
```json
{
  "date": "2026-03-12",
  "picks": [
    {
      "rank": 1,
      "ticker": "2330.TW",
      "name": "台積電",
      "nameEn": "TSMC",
      "market": "TW",
      "price": 1850,
      "currency": "TWD",
      "rating": "Buy",
      "target_price": 2100,
      "upside": "+13.5%",
      "scores": {
        "基本面": 9,
        "籌碼面": 7,
        "技術面": 8,
        "消息面": 8,
        "總經": 7,
        "產業展望": 9
      },
      "total_score": 48,
      "summary": "Earnings beat expectations...",
      "deep_report": "2330-2026-03-12.html"
    }
    // ... more picks (max 10) ...
  ]
}
```

### 3. Update JavaScript to load JSON
Replace the `loadPicksByDate` function:
```javascript
async function loadPicksByDate(type) {
  // ... date selection logic ...
  
  const dateStr = targetDate.toISOString().split('T')[0];
  try {
    const response = await fetch(`data/daily-picks-${dateStr}.json`);
    if (response.ok) {
      const data = await response.json();
      renderPicks(data.picks);
    } else {
      renderPicks([]); // Show empty state
    }
  } catch (error) {
    console.error('Failed to load picks:', error);
    renderPicks([]); // Graceful fallback
  }
}
```

---

## Troubleshooting

### Issue: Links to reports return 404
**Solution**: Verify HTML files are in same directory as index.html
```bash
ls -la /path/to/repo/*.html
# Should show: 1503, 1504, 1513, 1514, 2330, 2383 files
```

### Issue: Dashboard looks broken on mobile
**Solution**: Clear cache
```
Chrome: Ctrl+Shift+Del
Safari: Cmd+Shift+Del
Firefox: Ctrl+Shift+Del
```

### Issue: Date picker not working
**Solution**: Your browser might not support HTML5 date input. Use Chrome/Firefox/Safari (all modern versions support it).

### Issue: GitHub Pages not updating
**Solution**: GitHub needs 1-2 minutes to rebuild. Check:
1. Settings → Pages shows "Your site is live at..."
2. Actions tab shows successful deployment
3. Clear browser cache and reload

---

## Performance Notes

- Dashboard is 33 KB (very lightweight)
- All deep reports are separate HTML files (loaded on-demand)
- No external CDN dependencies (works offline)
- Fast load time even on 3G networks
- Mobile optimized with responsive design

---

## Security & Privacy

✅ No tracking scripts  
✅ No external API calls  
✅ No user data collection  
✅ All processing happens client-side  
✅ Safe to host on GitHub Pages  

---

## Future Enhancements

1. **API Integration**: Connect to real-time market data API
2. **Dark/Light Mode Toggle**: Add theme switcher
3. **Search**: Add ticker search functionality
4. **Filters**: Filter by rating, sector, market
5. **Charts**: Add price charts using Chart.js
6. **Export**: Export picks to CSV/PDF
7. **Push Notifications**: Notify on new picks

---

## Support

For issues or questions, check:
1. DASHBOARD_README.md (feature documentation)
2. Browser console (F12 → Console tab) for JavaScript errors
3. Network tab to verify JSON files load correctly

---

**Ready to deploy!** 🚀
