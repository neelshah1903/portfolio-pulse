# Portfolio Pulse

A live NSE stock portfolio tracker built with a Node.js scraping backend and a single-page dashboard frontend.

**Live site → [neelshah1903.github.io/portfolio-pulse](https://neelshah1903.github.io/portfolio-pulse/)**

---

## What it does

Add any NSE-listed stock ticker and instantly get a full quarterly financial breakdown — revenue, net profit, EPS, margins, and year-on-year growth — all pulled live from Screener.in.

### Dashboard features

- **Portfolio KPIs** — TTM revenue, TTM PAT, portfolio-level revenue growth % and PAT growth % for the latest reported quarter
- **Smart quarter alignment** — cross-stock comparisons only include stocks that have reported the latest quarter; stocks still pending show a ⏳ indicator and are excluded until their results drop
- **Stock chips with sparklines** — each holding shows an 8-quarter mini revenue trend at a glance
- **5 interactive charts**
  - Revenue trend (4Q / 8Q / 12Q toggle)
  - Net profit trend
  - Revenue YoY % bar chart
  - PAT YoY % bar chart
  - Net margin % trend
  - Rev vs PAT growth quadrant scatter (Star / Cash Cow / Turnaround / Laggard)
- **Sortable quarterly table** with TTM rows, colour-coded tickers, and YoY growth columns
- **CSV export** — one click downloads all data as a spreadsheet
- **LocalStorage persistence** — stocks are saved in the browser, so data survives page refreshes

---

## Architecture

| Layer | Tech | Hosted on |
|-------|------|-----------|
| Frontend | Vanilla HTML/CSS/JS + Chart.js | GitHub Pages |
| Backend | Node.js + Express + Cheerio | Render (free tier) |
| Data source | Screener.in (scraped) | — |

The backend proxy at `https://portfolio-proxy-976u.onrender.com` handles scraping so the frontend never hits Screener.in directly (avoiding CORS issues). It automatically falls back from consolidated to standalone financials for companies like insurance firms that don't publish consolidated results.

---

## Supported tickers

Any NSE ticker listed on Screener.in — banks (HDFCBANK, ICICIBANK, SBIN), IT (TCS, INFY, WIPRO), conglomerates (RELIANCE), insurance (ICICIGI), and more.

---

## Local usage

Just open `index.html` in any browser. No build step, no dependencies, no server needed on the frontend.