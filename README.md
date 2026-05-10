# Portfolio Pulse

A full-stack equity research dashboard for **Indian (NSE) and US stocks** — built by a CFA Level 3 candidate who got tired of switching between 5 different tabs to track fundamentals and macro.

**Live demo → https://neelshah1903.github.io/portfolio-pulse/**

![Portfolio Pulse Dashboard](screenshot.png)

---

## What it does

Add any NSE or US ticker and instantly see:
- Last 8–12 quarters of financials pulled from live sources
- Revenue, Net Profit, EPS, Operating Margin (OPM% for NSE / EBIT Margin for US), Net Margin
- YoY growth rates, TTM aggregates, and cross-stock comparisons
- A live macro dashboard with 8+ charts sourced from FRED and Yahoo Finance

Everything persists in your browser — no login, no account, no install.

---

## Features

### 📊 Market Watch Tab
Real-time macro environment in one place:

| Chart | Source | Detail |
|---|---|---|
| S&P 500 · Nasdaq · Dow Jones | FRED | Indexed to 100 (2-year trend) |
| US Treasury Yields (2Y & 10Y) | FRED | With yield spread — inverted curve flagged ⚠ |
| Yield Spread (10Y − 2Y) | FRED | Bar chart — green = normal, red = inverted |
| VIX Fear Index | FRED | With 20 (calm) and 30 (fear) reference lines |
| Inflation — Core PCE & CPI YoY | FRED | Fed's 2% target overlaid |
| Unemployment Rate | FRED | 2-year trend |
| Crude Oil — WTI & Brent | Yahoo Finance | Real-time futures prices |
| Fed Funds Rate | FRED | Monthly, 6-year history |

### 📈 Portfolio Analysis
- **KPI cards** — TTM Revenue, TTM Profit, portfolio YoY growth, best performer
- **Trend charts** — Revenue, Net Profit, and Operating Margin % across last 4/8/12 quarters
- **YoY bar charts** — Revenue and PAT growth, latest quarter, all holdings compared
- **Quadrant scatter** — Rev growth vs PAT growth mapped to Star / Cash Cow / Turnaround / Laggard
- **Sortable table** — all quarterly rows with OPM%, Net Margin, YoY, EPS

### 🌐 Macro Indicator Strip
Always-visible strip above all tabs:
`S&P 500 · Nasdaq · Dow Jones · Nikkei · 10Y · 2Y · Spread · Fed Rate · VIX · Core PCE · CPI · Unemployment · WTI · Brent`

### ✦ AI Portfolio Analyst
Ask natural language questions about your portfolio — powered by Llama 3.3 70B via Groq. Context-aware: knows your stocks' actual numbers.

### Holdings Chips
Each stock shows a mini revenue sparkline + YoY% at a glance. Pending-quarter stocks flagged with ⏳ and excluded from cross-stock comparisons until they report.

### CSV Export
Download all quarterly data for the active market view.

---

## Data sources

| Data | Source | Notes |
|---|---|---|
| 🇮🇳 NSE fundamentals | [Screener.in](https://www.screener.in) | Consolidated → Standalone fallback |
| 🇺🇸 US fundamentals | [Barchart.com](https://www.barchart.com) | Quarterly income statement |
| Indices, yields, VIX, inflation, unemployment | [FRED (St. Louis Fed)](https://fred.stlouisfed.org) | Free public API |
| WTI & Brent crude | Yahoo Finance | Front-month futures (CL=F, BZ=F) |
| AI answers | [Groq / Llama 3.3 70B](https://groq.com) | Portfolio context injected |

---

## Architecture

```
Browser (GitHub Pages)
    │
    ├── Chart.js 4 (charts)
    └── Vanilla JS → fetch()
            │
            ▼
    Node.js Proxy (Render)
            │
            ├── /stock  → scrapes Screener.in or Barchart
            ├── /macro  → FRED API + Yahoo Finance (4hr cache)
            ├── /macro-chart → FRED + Yahoo (4hr cache, 2yr history)
            └── /chat   → Groq API
```

**Frontend:** Vanilla HTML/CSS/JS · Chart.js 4 · GitHub Pages  
**Backend:** Node.js · Express · Cheerio · Render free tier  
**APIs:** FRED (macro) · Yahoo Finance (oil) · Groq (AI)  
**Storage:** Browser localStorage

---

## Running locally

```bash
# Backend
cd portfolio-proxy
npm install
FRED_API_KEY=your_key GROQ_API_KEY=your_key node index.js

# Frontend — just open portfolio-tracker.html in your browser
# (change PROXY in the HTML to http://localhost:3000)
```

---

## Limitations

- Render free tier spins down after inactivity — first fetch takes ~15s to wake up
- Scraping-dependent: breaks if Screener.in or Barchart change their HTML structure
- Mixed-currency portfolio KPIs (₹ + $) are hidden to avoid misleading aggregates
- Historical data limited to what the public pages show (~8–12 quarters)
