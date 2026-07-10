<div align="center">

# 🗓️ Changelog

*All notable changes to Ledger, grouped by release. Format loosely follows [Keep a Changelog](https://keepachangelog.com/).*

</div>

---

## 🚀 v3.1 — Smart Capture: Screenshots, Statements & Insights

### ✨ Added
- 📱 **Scan Screenshot** — direct AI-vision reading of UPI confirmations, transaction-history lists, and bank mini-statements, with multi-transaction detection in a single image
- 📤 **Share Target** — Ledger now registers as a native share destination once installed, so screenshots can be shared directly into the app from any payments app
- 📄 **Import Statement** — new `+` entry point accepting PDF, CSV, XLS, and XLSX bank statements, with chunked/async parsing for large files
- 🧠 **Shared AI Categorization Engine** — one categorization module now powers Scan Receipt, Scan Screenshot, Share Target, and Statement Import, reading directly from the user's own category list
- 🔍 **Document-Type Detection** — automatic classification of imports as receipt, invoice, UPI screenshot, or bank statement
- 🔀 **Multi-Entry Batch Review** — a shared review screen for every AI import, with inline editing, row deletion, row splitting, running totals, and a single "Add All" bulk-commit action
- 📊 **AI Spending Insights** — category breakdown, an AI-written spending narrative with real numbers and saving suggestions, cached to minimize API usage
- 📈 **Spending Trajectory Projections** — live end-of-week, end-of-2-weeks, and end-of-month run-rate forecasts against budget

### 🛠️ Fixed
- 🔑 Unified the AI API key lookup across every AI feature (categorization, statement import, screenshot vision, insights) to a single shared source, resolving cases where one flow couldn't find a key that another flow had already saved

---

## 🧩 v3.0 — Storage Resilience & Installability

### ✨ Added
- 💾 **Fallback storage engine** — automatic in-memory + `localStorage`-backed database swap-in for browsers without real IndexedDB support, with live storage-engine status shown in Settings
- 🖼️ **New themed icon set** — full favicon, Apple touch icon, and Android adaptive-icon (maskable) set matching the Ledger Dark visual identity
- 📱 Confirmed and finalized PWA installability (manifest + Workbox service worker) across Android/Chrome and iOS/Safari

---

## 🧠 v2.0 — Receipts, Insights & INR

### ✨ Added
- 🧾 **Full receipt OCR pipeline** — canvas preprocessing, Tesseract OCR, metadata exclusion filtering, anchor-priority total detection, and a mandatory review-before-save panel
- 🧠 **Merchant memory** — corrections made after a scan are remembered for that merchant going forward
- 🤖 **Optional AI fallback parsing** for handwritten receipts
- 📊 **Insights page** — running balance, budget burn-down, 12-month category trend, day-of-week spending, top merchants, full-year heatmap, savings-rate bars, net worth tracking, income-to-category Sankey diagram, financial health score, subscription audit, and end-of-month balance projection
- 🔍 Global fuzzy search, multi-tag chips with filtering, month-over-month category deltas, and anomaly flags on the Ledger view
- 🇮🇳 **INR-first formatting** (₹ with lakh/crore grouping) as the default locale

---

## 🏗️ v1.0 — Core Ledger

### ✨ Added
- 📝 Manual transaction entry, dashboard summary cards, ledger view, export/import, and filtering
- 🥧 Dashboard pie chart, 6-month bar trend, monthly budgets with progress bars and budget health
- 🔄 Recurring transactions with catch-up, multiple wallets, custom categories
- 📱 PWA manifest, icons, Workbox precaching, update-available toast, online/offline indicator
- 🎯 Goals with a featured rarity-bordered card and contribution tracking
- ❄️ Debt snowball planner with payoff timeline
- 🔥 No-spend streak tracking with a daily-reminder widget
- 🎙️ Voice entry, 📍 location tagging, and a personal Leaflet spending map
- 🧩 Draggable/hideable dashboard widget grid, full theming system (Light/Dark/Cyberpunk/High-Contrast) with accent picker
- 🗑️ Trash view with 30-day auto-purge, 7-day backup reminder, schema-versioned exports
