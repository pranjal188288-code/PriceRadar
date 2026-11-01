# ⚡ PriceRadar — Walkthrough & Verification

We built a full-stack **Multi-Platform Price Comparer & Graph Tracker** targeting major Indian e-commerce platforms: **Amazon India, Flipkart, Snapdeal, and Meesho**.

---

## 🌟 Key Accomplishments

### 1. 📊 Graph-Based Historical Price Tracking
- Integrated **Chart.js** multi-line historical trend visualization.
- **Dynamic Timeframes**: 7 Days, 15 Days, 30 Days, and 60 Days.
- **Interactive Platform Toggles**: Toggle Amazon, Flipkart, Snapdeal, or Meesho lines on the graph independently.
- **Period Records**: Dynamically pinpoints **All-Time Lowest Recorded Price** (with store name & date) and **All-Time Highest Recorded Price**.
- **Smart Buy Recommendation**: Analyzes price volatility and displays recommendations (e.g. *"Best Time to Buy! Price is near historic all-time low"* vs *"Consider waiting or setting an alert"*).

### 2. 🔴🟢 Highest & Lowest Price Intelligence
- Prominent side-by-side **Highest vs Lowest Price Analysis Banner**:
  - **Lowest Price Card** (Vibrant Emerald Glow): Displays the best deal store, price in ₹, % discount from MRP, available coupons, and direct checkout link.
  - **Savings Meter**: Shows exact rupee savings (e.g., *Save up to ₹3,645 by comparing stores*) and percentage price spread across platforms.
  - **Highest Price Card** (Crimson Warning): Flags the most expensive store and calculates how much a shopper would overpay without comparison.

### 3. 🛒 4-Platform Real-Time Quotes Grid
- Tailored price cards for:
  - 🟠 **Amazon India** (`Amazon.in` Prime delivery & bank cashbacks)
  - 🔵 **Flipkart** (SuperCoin / Big Billion Days discounts & exchange offers)
  - 🔴 **Snapdeal** (Value deals & clearance promos)
  - 🟣 **Meesho** (Direct wholesale rates & zero-commission pricing)
- Badges for **"Best Deal"**, **"Highest Store Price"**, and relative overpay calculations (`+₹X more than lowest store`).
- Stock status indicators (*In Stock* vs *Out of Stock*) and delivery promises.

### 4. 📋 Side-by-Side Platform Comparison Matrix
- Full comparison table detailing:
  - Store Platform & Trust score
  - Current price & MRP
  - Discount percentage
  - Market status badge (Lowest, Highest, Competitive)
  - Bank offers & coupons
  - Delivery timelines
  - Direct store purchase buttons

### 5. 🔍 Universal Search & Live URL Scraper
- Quick search across Electronics, Smartphones, Laptops, Audio, Footwear, Fashion, and Kitchen.
- Popular preset search chips (`iPhone 15`, `Galaxy S24 Ultra`, `Sony WH-1000XM5`, `MacBook Air M2`, `boAt Airdopes 141`, `Nike Air Jordan 1`).
- **Live URL Scraper Mode**: Allows users to paste any product URL from Amazon, Flipkart, Snapdeal, or Meesho to extract title/image and cross-reference across all 4 platforms.

### 6. 🔔 Price Drop Alerts
- Custom alert modal where users specify an email and target price threshold.
- Interactive celebration feedback via `canvas-confetti`.

### 7. 🎨 Rich Modern Aesthetics
- Dark mode default with instant Light mode toggle.
- Glassmorphism panels (`backdrop-filter: blur`), subtle gradients, ambient glowing backdrop, and typography powered by **Outfit** and **Plus Jakarta Sans**.

---

## 🏗️ Project Architecture

```
price-tracker/
├── backend/
│   ├── server.js            # Express API (ports 3001)
│   ├── scraper.js           # Live scraper & multi-platform price estimation engine
│   ├── data/products.js     # Catalog across Indian e-commerce & 30-day price history generator
│   └── package.json         # Express, CORS, Axios, Cheerio
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx                   # Brand logo, platform status pills, theme toggle
│   │   │   ├── SearchBar.jsx                # Search input, URL scraper tab, chips, categories
│   │   │   ├── HighLowBanner.jsx            # Highest vs Lowest price comparison banner
│   │   │   ├── PriceChart.jsx               # Chart.js multi-line history graph
│   │   │   ├── PlatformPriceCard.jsx        # Amazon, Flipkart, Snapdeal, Meesho cards
│   │   │   ├── PlatformComparisonTable.jsx  # Side-by-side full matrix
│   │   │   ├── ProductSummaryHeader.jsx     # Product hero, gallery, specs, rating
│   │   │   ├── ProductCard.jsx              # Search result cards with mini high/low bars
│   │   │   ├── TrendingDeals.jsx            # Biggest price drop showcase
│   │   │   ├── PriceAlertModal.jsx          # Price drop alert subscription modal
│   │   │   └── SupportedPlatformsView.jsx   # Architectural platform details
│   │   ├── App.jsx          # Main application coordinator
│   │   ├── App.css          # Responsive styling & glassmorphism system
│   │   └── index.css        # Theme tokens, dark/light styles, animations
│   ├── vite.config.js       # Vite configuration with API proxy to backend
│   └── package.json         # React 18, Vite, Chart.js, Lucide, Confetti
└── package.json             # Monorepo runner (concurrently)
```

---

## 🧪 Verification Results

| Check | Result |
|---|---|
| **Production Build (`npm run build`)** | ✅ Built client bundle in 4.21s with 0 errors |
| **Backend API (`/api/products`)** | ✅ Returned enriched catalog with calculated high/low stats |
| **Historical Graph API (`/api/history/prod-1?days=7`)** | ✅ Generated date-by-date prices for all 4 stores, all-time high, all-time low |
| **Frontend Web Server (`http://localhost:5173/`)** | ✅ HTTP 200 OK, title and React refresh hook injected cleanly |
| **Vite Dev Proxy** | ✅ Forwarding `/api/*` to Express backend on port 3001 |

---

## 🚀 How to Run

To run both Frontend and Backend concurrently with one command:

```bash
cd price-tracker
npm run dev
```

- **Frontend**: [http://localhost:5173](http://localhost:5173)
- **Backend API**: [http://localhost:3001](http://localhost:3001)
