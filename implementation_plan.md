# Price Comparer & Tracker — Full Stack App

A modern React + Vite price comparison and tracking platform targeting Indian e-commerce stores (Amazon IN, Flipkart, Snapdeal, Meesho).

---

## User Review Required

> [!IMPORTANT]
> **Web Scraping Limitation**: Live web scraping of Amazon, Flipkart, Snapdeal, and Meesho is blocked by bot-protection systems (CAPTCHAs, Cloudflare, JS challenges). A pure scraping backend would be unreliable and could violate their ToS. 
>
> **Recommended Hybrid Approach**: The backend will use **realistic mock/simulated price data** for the demo, with a clear architecture that allows easy plug-in of real APIs (e.g., RapidAPI's Amazon/Flipkart Price APIs) later. This is the standard approach used by most price-tracking tools initially.

> [!WARNING]
> **Node.js Required**: The React + Vite frontend requires Node.js (v18+) installed on your machine. The backend will use Node.js + Express.

---

## Open Questions

> [!NOTE]
> These are answered by defaults — no action needed unless you want to change them:
> - Currency: **INR (₹)**
> - Price history: Stored in-memory (resets on server restart) — for persistence, a database would be needed
> - Chart library: **Chart.js** (lightweight, no extra setup)

---

## Architecture Overview

```
┌─────────────────────────────────────────┐
│         Frontend (React + Vite)          │
│  - Product Search                        │
│  - Platform Price Cards                  │
│  - Price History Graph (Chart.js)        │
│  - Best Deal Highlight                   │
│  - Highest / Lowest Price Badges         │
└──────────────┬──────────────────────────┘
               │ HTTP (REST API)
┌──────────────▼──────────────────────────┐
│         Backend (Node.js + Express)      │
│  - /api/search?q=<product>              │
│  - /api/history/:productId              │
│  - Simulated price data per platform    │
└─────────────────────────────────────────┘
```

---

## Proposed Changes

### Backend — `c:\Users\singh\.antigravity-ide\price-tracker\backend\`

#### [NEW] `server.js`
- Express server on port `3001`
- Routes: `/api/search`, `/api/history/:id`, `/api/platforms`
- Generates realistic price data with variation across platforms
- Simulates price history (30-day data points) with realistic fluctuations

#### [NEW] `data/products.js`
- 50+ sample products across Electronics, Fashion, Groceries categories
- Platform-specific pricing logic (e.g., Meesho tends to be cheaper for fashion)

#### [NEW] `package.json` (backend)

---

### Frontend — `c:\Users\singh\.antigravity-ide\price-tracker\frontend\`

#### [NEW] React + Vite app (via `npx create-vite`)

#### [NEW] `src/App.jsx` — Root component with routing

#### [NEW] `src/pages/HomePage.jsx`
- Hero section with search bar
- Featured products / trending deals

#### [NEW] `src/pages/SearchResultsPage.jsx`
- Platform price cards (Amazon, Flipkart, Snapdeal, Meesho)
- **Highest price** badge (red) and **lowest price** badge (green)
- Best deal CTA with direct platform link

#### [NEW] `src/pages/ProductDetailPage.jsx`
- Price history graph (30-day line chart via Chart.js)
- All-time high / all-time low prices
- Price drop alerts section
- Platform comparison table

#### [NEW] `src/components/`
- `PriceCard.jsx` — Per-platform price display
- `PriceChart.jsx` — Chart.js line graph with multi-platform overlay
- `PlatformBadge.jsx` — Platform logo + price badge
- `HighLowBanner.jsx` — Highest/Lowest price banner
- `SearchBar.jsx` — Animated search with suggestions
- `Navbar.jsx` — Navigation with dark mode toggle

#### [NEW] `src/index.css` — Design system
- Dark mode by default (toggle to light)
- Color palette: Deep navy + electric blue + amber accents
- Glassmorphism cards
- Smooth animations

---

## Key Features

| Feature | Details |
|---|---|
| 🔍 **Product Search** | Search any product, get results across all 4 platforms |
| 💰 **Price Comparison Cards** | Side-by-side platform prices with savings calculation |
| 🏆 **Best Deal Highlight** | Prominent "Best Price" badge on lowest-price platform |
| 📈 **Price History Graph** | 30-day chart showing price trends per platform |
| 🔴🟢 **High/Low Indicators** | All-time high (red) and all-time low (green) markers |
| 🌙 **Dark/Light Mode** | Toggle between themes |
| 📱 **Responsive** | Works on mobile, tablet, desktop |
| ⚡ **Fast Search** | Debounced search with loading animations |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 + Vite 5 |
| Routing | React Router v6 |
| Charts | Chart.js + react-chartjs-2 |
| Styling | Vanilla CSS with CSS variables |
| Icons | Lucide React |
| Backend | Node.js + Express |
| HTTP Client | Axios |
| Dev tooling | Concurrently (run both servers) |

---

## Verification Plan

### Automated Tests
- `npm run dev` — starts both frontend (port 5173) and backend (port 3001)
- API test: `curl http://localhost:3001/api/search?q=iphone`

### Manual Verification
- Search for a product → see platform price cards
- Click a product → see 30-day price chart
- Verify highest/lowest price badges appear correctly
- Toggle dark/light mode
- Test on mobile viewport
