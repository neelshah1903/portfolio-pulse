# Portfolio Pulse

A clean, dark-themed stock portfolio tracker for **Indian (NSE)** and **US** equities — built as a single HTML file with no install required.

**Live:** https://neelshah1903.github.io/portfolio-pulse/

---

## What it does

- Add any NSE or US stock ticker and instantly pull the last 8–12 quarters of financials
- Separate **🇮🇳 India** and **🇺🇸 US** dashboard views — no mixing of markets in charts
- Quarterly data: Revenue, Net Profit, EPS, Net Margin
- Cross-stock comparisons only include stocks that have **reported the latest quarter** — stocks still pending are flagged with ⏳ and excluded from YoY charts and the scatter quadrant until results are out
- Everything saved to browser localStorage — your portfolio persists across sessions

## Features

### KPI Cards
- Portfolio TTM Revenue & Net Profit (auto-formatted: ₹ Cr / $ M / $ B)
- Portfolio Revenue & PAT YoY growth (vs same quarter last year)
- Best revenue and PAT performer of the quarter

### Charts
| Chart | Description |
|---|---|
| Revenue Trend | Line chart — 4Q / 8Q / 12Q toggle |
| Net Profit Trend | Line chart with same period |
| Revenue YoY % | Bar chart — latest quarter only, qualified stocks |
| PAT YoY % | Bar chart — latest quarter only, qualified stocks |
| Net Margin % | Multi-line trend — last 8 quarters |
| Quadrant (Scatter) | Rev growth vs PAT growth — Star / Cash Cow / Turnaround / Laggard |

### Holdings chips
Each stock shows a mini revenue sparkline and the YoY revenue growth % at a glance.

### Quarterly table
Sortable by any column. Includes TTM rows. Hover on Revenue/Profit cells to see the unit (₹ Cr or $ M).

### CSV Export
Downloads all quarterly data for the active market view.

---

## How to use

1. Open https://neelshah1903.github.io/portfolio-pulse/
2. Select **🇮🇳 India** or **🇺🇸 US** from the dropdown
3. Type a ticker (e.g. `HDFCBANK`, `AAPL`) and click **+ Add Stock**
4. Switch between **All / India / US** tabs to isolate each market's dashboard

Your portfolio is saved in your browser — no account needed.

---

## Data sources

| Market | Source | Data |
|---|---|---|
| 🇮🇳 NSE | [Screener.in](https://www.screener.in) | Consolidated → Standalone fallback |
| 🇺🇸 US | [Barchart.com](https://www.barchart.com) | Quarterly income statement |

Fetched via a lightweight Node.js proxy ([portfolio-proxy](https://github.com/neelshah1903/portfolio-proxy)) hosted on Render.

---

## Tech stack

- **Frontend:** Vanilla HTML/CSS/JS — zero frameworks, zero dependencies
- **Charts:** [Chart.js 4](https://www.chartjs.org/)
- **Backend proxy:** Node.js + Express + Cheerio (HTML scraping)
- **Hosting:** GitHub Pages (frontend) + Render free tier (proxy)
- **Storage:** Browser localStorage

---

## Limitations

- Render free tier spins down after inactivity — first stock fetch may take ~15 seconds to wake up
- US stock data depends on Barchart.com page structure; may break if they change their layout
- Currencies are not converted — India stocks are in ₹ Crore, US stocks in $ Million; mixed-market KPI totals are hidden to avoid misleading sums
- Historical data limited to what Screener.in / Barchart shows publicly (typically 8–12 quarters)