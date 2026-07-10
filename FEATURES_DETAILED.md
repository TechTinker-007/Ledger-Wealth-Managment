<div align="center">

# 📖 Ledger — Detailed Feature Guide

*Everything Ledger does, and how it does it.*

</div>

---

## 📑 Contents

1. [📥 Capture & Import Pipeline](#-capture--import-pipeline)
2. [🧠 AI Categorization Engine](#-ai-categorization-engine)
3. [🔀 Batch Review & Bulk Add](#-batch-review--bulk-add)
4. [📊 Insights & Spending Trajectory](#-insights--spending-trajectory)
5. [📋 Core Ledger & Dashboard](#-core-ledger--dashboard)
6. [🎯 Goals, Debt & Recurring](#-goals-debt--recurring)
7. [🎨 Theming & Personalization](#-theming--personalization)
8. [🛡️ Data Safety & Storage](#️-data-safety--storage)
9. [🗺️ Extras](#️-extras)

---

## 📥 Capture & Import Pipeline

Ledger gives you **five distinct doors in** for a transaction, all of which funnel into the same underlying AI engine and the same review screen — so no matter how a transaction gets in, the experience of confirming it feels identical.

### 🧾 Scan Receipt
The original capture flow. A photo or upload runs through an on-device preprocessing pass (grayscale conversion, contrast stretching, binarization, upscaling of tiny crops) before Tesseract OCR reads the text. A rules engine then strips out anything that isn't the actual purchase — GST numbers, phone numbers, invoice references, dates, pincodes — and locates the true total using an anchor-priority search (Grand Total beats Net/Payable beats plain Total, with the *last* match winning, since the grand total typically prints last and lowest). Nothing is ever auto-submitted: every scan lands on a review panel with a visible confidence badge and a short trail of how the number was chosen. Expect roughly 85–90% field accuracy on printed thermal receipts; handwritten receipts lean on an optional AI fallback instead.

### 📱 Scan Screenshot
Where OCR struggles — small, stylized UI text in UPI apps and banking apps — Ledger switches strategy entirely. Instead of extracting text first, the screenshot is sent **directly to a vision-capable AI model**, which reads the image the way a person would. It's built to handle three shapes of input without being told which one it's looking at:
- A single UPI payment confirmation (one transaction)
- A UPI app's transaction-history list (many transactions, mixed categories and amounts)
- A bank app's mini-statement view (several rows at once)

Every distinct transaction visible in the image is listed out separately — the model is explicitly instructed never to merge multiple transactions into one, and never to invent a row that isn't actually shown.

### 📤 Share Target
Ledger registers itself as a native **share destination** on your phone once installed as a PWA. That means after completing a UPI payment, hitting your payment app's "Share" button will show Ledger right alongside WhatsApp, Gmail, and your other apps. Tapping it hands the screenshot straight to the same vision pipeline used by Scan Screenshot — no manual file picking, no app switching. (This only appears once Ledger is added to your home screen; browser tabs can't register as share targets.)

### 📄 Import Bank Statement
A dedicated "+" import button accepts PDF, CSV, XLS, and XLSX statements. CSV and Excel files are parsed natively in the browser, with automatic detection of date, description, and amount columns (handling both a single signed "amount" column and separate debit/credit columns). PDF statements are read with client-side text extraction that preserves row structure, then handed to the AI to be split into individual transactions. Everything happens in chunks so a statement with hundreds of rows never freezes the interface.

### ✍️ Manual Entry
The original, always-available fallback — a full entry form with smart autocomplete, multi-tag support (`#vacation #reimbursable`), optional voice input, and optional location tagging for the personal spending map.

---

## 🧠 AI Categorization Engine

Every transaction that comes in through *any* of the above doors — scanned, shared, imported, or statement-extracted — passes through one shared categorization engine:

- 🏷️ Categories are pulled **live from your own category list**, never hardcoded — the AI can only choose from categories you actually have, plus an "Uncategorized" fallback when it isn't confident
- 📦 **Batched requests** — statements with dozens of transactions are grouped into batches per API call rather than one call per row, keeping things fast and well within free-tier rate limits
- 🔀 **Mixed-category awareness** — a single bank statement or screenshot can (and usually does) contain groceries, subscriptions, rent, and dining in one file; every row is categorized independently rather than assuming one category per document
- 🔍 **Document-type detection** — a deterministic heuristic (checking for GST numbers, invoice line-items, UPI/UTR references, and date density) labels each batch as a receipt, invoice, UPI screenshot, or bank statement, so the review screen can show the right context even if the AI is temporarily unavailable
- 🛡️ **Fails safe** — a malformed or missing AI response never crashes the import; affected rows simply fall back to "Uncategorized" so you can sort them yourself

---

## 🔀 Batch Review & Bulk Add

However a transaction arrives, it lands on the same review screen before it ever touches your ledger:

- 📝 Every detected transaction is its own **editable row** — date, amount, description, and category can all be corrected inline
- ⚠️ **Low-confidence entries are visually flagged**, so you know exactly which rows deserve a second look before confirming
- ➗ **Split** a row if the AI merged two transactions into one by mistake
- 🗑️ **Delete** any row that isn't actually a transaction (a header line misread as a row, for example)
- 🧮 A **running total and entry count** update live, so you can sanity-check the batch against your actual bank statement total before committing
- ⚡ **One "Add All" button** commits every confirmed row to your ledger in a single database transaction — built to stay smooth even with 50–200+ rows from a long statement import
- 🖼️ A small badge on the review screen shows what kind of document was detected (Receipt / Invoice / UPI Screenshot / Bank Statement), so context is never lost

---

## 📊 Insights & Spending Trajectory

### 🥧 Category Breakdown
Plain-arithmetic aggregation (no AI needed) of your spend by category, for any window — this week, this month, or a custom range.

### 📈 Spending Trajectory
Three live projections, recalculated every time a transaction is added:
- **End of this week**
- **End of the next 2 weeks**
- **End of this month**

Each uses a simple, transparent run-rate calculation — *(spend so far ÷ days elapsed) × total days in the period* — shown alongside a progress bar against your budget, if you've set one.

### 💬 AI-Written Spending Summary
Once a day (or whenever your spending numbers actually change — not on every dashboard visit, to stay well within free-tier limits), Ledger asks its AI model for a short, numbers-grounded narrative: which 2–3 categories are driving your spend, whether any category has genuinely spiked compared to the previous period, and 2–3 saving suggestions that reference your real category names and amounts rather than generic advice like "track your spending more."

### 🏆 Deeper Analytics
The dedicated Insights page goes further, with a running balance line, per-category budget burn-down (ideal pace vs. actual), a 12-month stacked category trend, day-of-week spending patterns, your top merchants, a full-year spending calendar heatmap, savings-rate bars, net worth over time (cash plus goals minus debts), an income-to-category Sankey diagram, a graded financial health score, an automatic subscription audit (flagging repeating same-amount charges and annualizing their cost), and an end-of-month balance projection.

---

## 📋 Core Ledger & Dashboard

- 🔍 **Global fuzzy search** across description, tags, and amount
- 🏷️ **Multi-tag chips** on every transaction, with a tag filter row
- 📊 **Month-over-month deltas** shown directly on category chips
- 🚩 **Anomaly flags** on transactions that sit far outside your normal spending pattern for that category
- 🧩 **Draggable, hideable dashboard widgets** — arrange your dashboard exactly how you want it, with your layout remembered
- 🥧 Pie charts, a 6-month bar trend, and budget progress bars, all on the dashboard

---

## 🎯 Goals, Debt & Recurring

- 🎯 **Savings goals** with contribution tracking; your top goal gets a special rarity-bordered featured card
- ❄️ **Debt snowball planner** with a visual payoff timeline
- 🔄 **Recurring transactions**, including automatic catch-up if the app wasn't opened for a while
- 👛 **Multiple wallets** with per-wallet breakdowns and quick filtering
- 🔥 **No-spend streak tracking** — transactions marked "Essential" don't break your streak, and goal contributions are auto-marked essential

---

## 🎨 Theming & Personalization

- 🌗 **Light, Dark, Cyberpunk, and High-Contrast** themes, plus a custom accent color picker
- 🇮🇳 **INR-first formatting** by default — ₹ with proper lakh/crore grouping (₹1,23,45,678.50) — with a Settings override for any other currency via full `Intl` support
- 📱 Fully **installable as a PWA** on both Android/Chrome and iOS/Safari, with offline support and an update-available toast

---

## 🛡️ Data Safety & Storage

- 💾 **Local-first storage** via Dexie.js on top of IndexedDB — no practical size cap in normal use
- 🔁 **Automatic fallback engine** — if a browser doesn't expose real IndexedDB (some locked-down in-app browsers or hardened privacy modes), Ledger transparently swaps in an in-memory database and mirrors every write to `localStorage`, so nothing is lost — Settings shows a live badge for which storage engine is active
- 📤 **Full export/import** (JSON, with schema versioning) — the dashboard reminds you after 7 days without a backup
- 🗑️ **Trash view** with a 30-day auto-purge for deleted transactions
- 🔑 **Bring-your-own AI key** — your Groq (and optional Anthropic fallback) key lives only in your device's local storage and is used to call the AI provider directly from your browser

---

## 🗺️ Extras

- 🎙️ **Voice entry** for hands-free transaction logging
- 📍 **Location tagging** with a personal Leaflet-powered spending map — your coordinates never leave your device
- ⏰ **Daily reminder** to log spending (fires while the app is open or installed, since browsers don't allow true background scheduling from a PWA)
