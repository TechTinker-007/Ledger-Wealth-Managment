<div align="center">

# 💰 Ledger

### Your money, your device, your rules.

**An offline-first personal finance PWA that reads your receipts, your screenshots, and your bank statements — so you don't have to type a single number.**

[![Made with React](https://img.shields.io/badge/React-19-149ECA?logo=react&logoColor=white&style=for-the-badge)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-Strict-3178C6?logo=typescript&logoColor=white&style=for-the-badge)](https://www.typescriptlang.org)
[![Vite](https://img.shields.io/badge/Vite-8-646CFF?logo=vite&logoColor=white&style=for-the-badge)](https://vitejs.dev)
[![PWA](https://img.shields.io/badge/PWA-Installable-5A0FC8?logo=pwa&logoColor=white&style=for-the-badge)](#-privacy--offline-first)
[![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-DB4035?style=for-the-badge)](./LICENSE)

**[🚀 Open Live App] -->> https://ledger-five-rouge.vercel.app/(#)** &nbsp;·&nbsp; **[✨ Features](./FEATURES.md)** &nbsp;·&nbsp; **[📖 Full Feature Guide](./FEATURES_DETAILED.md)** &nbsp;·&nbsp; **[💭 About](./ABOUT.md)**

</div>

---

## 🧭 Table of Contents

- [What is Ledger?](#-what-is-ledger)
- [✨ Highlights](#-highlights)
- [🧠 How Ledger "Sees" Your Money](#-how-ledger-sees-your-money)
- [📥 Five Ways In](#-five-ways-in)
- [📊 Insights, Not Just Numbers](#-insights-not-just-numbers)
- [🏗️ Tech Stack](#️-tech-stack)
- [🔒 Privacy & Offline-First](#-privacy--offline-first)
- [📚 Documentation](#-documentation)
- [📄 License](#-license)

---

## 💡 What is Ledger?

Ledger is a **personal finance tracker that lives entirely on your phone** — no server, no account, no company reading your bank statements. It started as a simple expense logger and grew into something a lot more capable: point it at a receipt, a UPI payment screenshot, or a full bank statement PDF, and it reads the transactions out, sorts them into categories on its own, and hands you a clean list to confirm with one tap.

Everything renders in a custom **"Ledger Dark"** interface — deep charcoal surfaces, a violet accent (`#6C5CE7`), and Inter typography — built to feel calm even when your spreadsheet-brain wouldn't.

---

## ✨ Highlights

> 🧾 **Scan any receipt** — printed or handwritten, OCR + AI fills the form for you
> 📱 **Scan any screenshot** — UPI confirmations, payment histories, mini-statements, all in one shot
> 📤 **Share-to-Ledger** — send a screenshot straight from your UPI app's share sheet, no app-switching
> 📄 **Import full bank statements** — PDF, CSV, or Excel, hundreds of rows parsed in seconds
> 🧠 **AI auto-categorization** — every transaction gets sorted into the right bucket, automatically
> 🔀 **Multi-entry batch review** — one screenshot, ten transactions, ten editable rows, one "Add All"
> 📈 **Spending trajectory** — see where your week/fortnight/month is *headed*, before it happens
> 💬 **AI-written insights** — plain-English spending summaries with real numbers, not generic tips
> 🌐 **100% offline-capable** — your data never leaves your device unless you export it yourself

Full list → **[FEATURES.md](./FEATURES.md)**
Deep dive on every feature → **[FEATURES_DETAILED.md](./FEATURES_DETAILED.md)**

---

## 🧠 How Ledger "Sees" Your Money

Ledger runs on a **shared AI pipeline** that every entry point feeds into — so a receipt, a screenshot, and a bank statement all end up going through the same brain:

```
📄 / 📱 / 🧾  →  Extraction  →  🧠 AI Categorization  →  📝 Batch Review  →  ✅ Add All
```

| Stage | What happens |
|---|---|
| **Extraction** | Receipts run through on-device OCR; screenshots go straight to a vision-capable AI model (no OCR needed); statements are parsed natively from CSV/XLSX or PDF text |
| **AI Categorization** | Every single transaction — even ones mixed across ten different categories in one file — gets matched against *your own* category list |
| **Document Detection** | Ledger automatically figures out whether it's looking at a receipt, an invoice, a UPI screenshot, or a bank statement, and labels the batch accordingly |
| **Batch Review** | Every detected transaction becomes its own editable row — fix anything the AI misread, delete false positives, split merged rows |
| **Add All** | One tap commits everything to your on-device ledger in a single, fast transaction |

---

## 📥 Five Ways In

<table>
<tr><td>🧾</td><td><b>Scan Receipt</b></td><td>Snap or upload a receipt — OCR + AI fills the form, you just confirm</td></tr>
<tr><td>📱</td><td><b>Scan Screenshot</b></td><td>UPI payments, transaction history lists, bank mini-statements — read directly by AI vision</td></tr>
<tr><td>📤</td><td><b>Share Target</b></td><td>Hit "Share" on any screenshot from your payments app — Ledger shows up right in the share sheet</td></tr>
<tr><td>📄</td><td><b>Import Statement</b></td><td>Drop in a PDF, CSV, or Excel bank statement — hundreds of rows, auto-categorized</td></tr>
<tr><td>✍️</td><td><b>Manual Entry</b></td><td>The classic way — full control, voice entry and location tagging included</td></tr>
</table>

---

## 📊 Insights, Not Just Numbers

Ledger doesn't just log what you spent — it tells you **where it's going and where it's headed**:

- 🥧 **Category breakdown** — this week, this month, or any custom range
- 📈 **Trajectory projections** — end-of-week, end-of-2-weeks, and end-of-month spend forecasts, recalculated live as you add transactions
- 💬 **AI-written summary** — "Food delivery is 22% of spend this month, up from 14% last month" — real numbers, not "you should budget more"
- 💡 **Saving suggestions** — grounded in your actual category data, refreshed daily (not on every visit, to stay light on API usage)
- 🏆 **Financial health score**, subscription audit, anomaly flags, net-worth tracking, and a full spending calendar heatmap

---

## 🏗️ Tech Stack

<div align="center">

| Layer | Technology |
|---|---|
| **UI** | React 19 · TypeScript · Tailwind CSS v4 |
| **Build** | Vite 8 · vite-plugin-pwa (Workbox) |
| **Storage** | Dexie.js (IndexedDB) with an automatic in-memory + `localStorage` fallback engine |
| **Charts** | Recharts |
| **Receipt OCR** | Tesseract.js (lazy-loaded, on-device) |
| **Screenshot Reading** | Groq vision model (`meta-llama/llama-4-scout-17b-16e-instruct`) |
| **Categorization & Insights AI** | Groq (`llama-3.3-70b-versatile`) |
| **Statement Parsing** | SheetJS (CSV/XLSX) · pdf.js (PDF text extraction) |
| **Maps** | Leaflet + OpenStreetMap |
| **Drag & Drop** | dnd-kit |
| **Hosting** | Static deploy — GitHub Pages / Vercel, zero backend |

</div>

---

## 🔒 Privacy & Offline-First

- 📴 **Works fully offline** after first load — no connection needed for day-to-day use
- 💾 **All data stays on your device** in IndexedDB (or a `localStorage` fallback on locked-down browsers) — nothing is synced to any server
- 🔑 **Bring-your-own AI key** — your Groq key is stored only in your device's local storage and used to call Groq directly from your browser; Ledger's own infrastructure never sees your data or your key
- 📍 **Location tagging** (optional) never leaves your device — used only to plot your own spending map locally
- 📤 **Export anytime** — full JSON export/import so you always own your data

Since this is a static app with no backend, treat any in-app access gate as a *convenience*, not a security boundary — the real protection here is that your data simply never leaves your phone.

---

## 📚 Documentation

| Doc | What's inside |
|---|---|
| 📋 [FEATURES.md](./FEATURES.md) | Quick-scan feature list |
| 📖 [FEATURES_DETAILED.md](./FEATURES_DETAILED.md) | Every feature, explained in depth |
| 📝 [DESCRIPTION.md](./DESCRIPTION.md) | Short-form project description |
| 🗓️ [CHANGELOG.md](./CHANGELOG.md) | Version history |
| ⚖️ [LICENSE](./LICENSE) | Usage terms |

---

## 📄 License

This project is shared under an **All Rights Reserved** license. See **[LICENSE](./LICENSE)** for full terms.

---

<div align="center">

**Built solo, for personal use — one commit at a time. 💜**

</div>
