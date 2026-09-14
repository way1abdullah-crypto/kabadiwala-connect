## Kabadiwala Connect ##

"Bringing India's informal e-waste collectors into the formal recycling chain."

Built for "Smart India Hackathon 2026" — Problem Statement **SIH26229**, sponsored by the "Ministry of Mines (JNARDDC)".

---

# The Problem

India generates over 3,200 kilotonnes of e-waste every year — the third-highest volume globally. Yet only around 1% of it moves through formal, authorized recycling channels. The rest flows through an informal network of collectors (*kabadiwalas*) who have:

- No reliable way to know fair, current market prices for what they collect
- No visibility into which recyclers nearby are actually authorized under the E-Waste (Management) Rules, 2022
- No digital trail of who handed over what, when, and to whom

This isn't a small gap — it's a national blind spot that costs collectors fair income, costs the country recoverable materials (copper, gold, platinum), and leaves hazardous e-waste flowing into unsafe backyard processing (open cable burning, acid leaching of PCBs).

# What We Built

Kabadiwala Connect is a multilingual, voice-first platform connecting four user types into one traceable chain:

Household/Customer → Informal Collector → Local Agent → Authorized Recycler.

### Core features

- **Voice-first, trilingual interface** (English, Hindi, Kannada) with zero-literacy-barrier design — icon-based navigation, audio playback for every rate and receipt
- **Real-time fair-price discovery** so collectors know what their material is actually worth before selling
- **Digital transaction records** — every sale generates a receipt with transaction ID, material, weight, and payment method (cash or UPI), so cash transactions still leave a verifiable digital trail
- **Material Passport** — a QR-coded chain-of-custody record tracking material from Collected → Aggregated → Transported → Received by Recycler → Processed
- **Agent-assisted mode** for collectors without smartphones — a local agent (scrap-shop owner, SHG member) performs the digital steps on their behalf, so no one is excluded from the formal system
- **Recycler/Admin dashboards** with a live map of material flow, lot browsing, and verification tools

## Why These Design Decisions

**Why voice-first, not just multilingual text?**
Our target users often have low or no literacy. A translated UI alone doesn't solve that — every price, receipt, and instruction needed to be audible, not just readable.

**Why hash-chained records instead of a full blockchain?**
For a chain-of-custody system at this stage, we didn't need blockchain's decentralization guarantees — we needed tamper-evidence and a low-cost, easy-to-audit trail. A hash-chained log backed by a normal database gets us that without the operational overhead. This is a trade-off, not a limitation we didn't consider — full DLT is a reasonable stretch goal if the system needs multi-party trust guarantees at scale.

**Why require digital proof even for cash transactions?**
Most collectors depend on cash, so we never made digital payment mandatory. But every cash transaction still needs a transaction ID and confirmation record — otherwise the traceability promise of the Material Passport breaks the moment cash changes hands.

**Why an agent-assisted path instead of requiring smartphones?**
Assuming smartphone ownership would exclude a large share of the actual target population. The agent model — plus an SMS/IVR fallback for rate-checks — keeps the system usable by everyone, not just the digitally fluent minority.

## Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Mobile (Collector/Agent) | React Native + TypeScript | Android-first reach, single codebase |
| Web (Recycler/Admin) | React + TypeScript | Data-dense dashboards, responsive |
| Backend | Node.js + NestJS | Modular monolith, scales to microservices later without a rewrite |
| Database | PostgreSQL | Relational integrity for transactions, lots, and audit logs |
| Offline storage | SQLite | Local-first transaction storage with auto-sync |
| Auth | OTP-based, role-based access | Simple, no password friction for low-tech-literacy users |
| Maps | OpenStreetMap / Leaflet | Free, no API key, live material-flow visualization |

## What's Not Built Yet (and why)

Being upfront about scope, since a hackathon build is a prototype, not a finished product:

- **Hazard-model training from raw satellite/market data** — out of scope; we consume simplified/reference pricing rather than building a live commodity-pricing pipeline from scratch
- **Full production-grade encryption/key management** — the demo shows the pattern (hashing, tamper-evidence) rather than a hardened KMS deployment
- **Live SMS/IVR gateway integration** — currently mocked; the architecture supports it, but a real telecom integration needs a paid gateway account we didn't provision for the demo

## Team

ABDULLAH HEDAYAT- Team leader and developer

## Running the Project

```bash
# clone the repo
git clone <repo-url>
cd kabadiwala-connect

# install dependencies
npm install

# run locally
npm run dev
```

---

"Built for SIH 2026. This repository reflects our actual design process — including the trade-offs above — and we're happy to walk through any part of the architecture in detail".
