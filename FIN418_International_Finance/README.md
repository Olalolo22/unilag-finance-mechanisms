# FIN 418: International Business Finance

**Department:** Finance | **Units:** 3 | **Exam Mode:** Written (Theory)

---

## 1. Course Overview & Core TradFi Topics
FIN 418 covers international financial systems, currency dynamics, and corporate foreign exchange risk:
* **Exchange Rate Determination:** Purchasing Power Parity (PPP), Absolute and Relative PPP.
* **Interest Rate Parities:** Covered Interest Rate Parity (CIRP) and Uncovered Interest Rate Parity (UIRP).
* **International Financial Markets & Institutions:** Eurocurrency markets, international bond markets, IMF, World Bank, foreign exchange swap desks.
* **Balance of Payments (BOP):** Current account, capital account, official reserves account, and balance of payment deficits/surpluses.
* **Foreign Exchange Exposure & Hedging:** Transaction, translation, and economic exposure. Hedging using forward contracts, futures, currency options, and money market hedges.

---

## 2. The On-Chain Mechanism Analogue

### A. Covered Interest Rate Parity (CIRP) & Cross-Chain Yield Arbitrage
* **TradFi Formula:** `F / S = (1 + r_d) / (1 + r_f)`
  * `F` = Forward exchange rate
  * `S` = Spot exchange rate
  * `r_d` = Domestic interest rate
  * `r_f` = Foreign interest rate
* **Protocol Analogue:** Cross-chain interest rate arbitrage and perpetual funding rates. When the yield on Base USDC differs from Solana USDC, or when a synthetic perp price diverges from the spot oracle, the funding rate acts as the continuous interest rate parity adjustment that forces the perp price to anchor back to spot.

### B. Balance of Payments (BOP) & Cross-Chain Bridge Invariants
* **TradFi:** Current Account Deficits must be balanced by Capital Account Inflows or Reserve Drawdowns.
* **Protocol Analogue:** Liquidity imbalances in cross-chain bridges (e.g. Stargate / Circle CCTP / RouteDock). When order flow heavily drains USDC on Solana into Ethereum, the bridge's local reserve depletes. The bridge protocol must implement dynamic rebalancing fees (pricing curves) to incentivize arbitrageurs to route capital back.

### C. FX AMMs & Stablecoin Peg Mechanisms
* **TradFi:** Central bank foreign exchange reserves defending a currency peg against speculative attacks.
* **Protocol Analogue:** Curve Finance Stableswap invariant (`A * sum(x_i) + D = A * D * n^n + D^(n+1) / (n^n * prod(x_i))`). Concentrating liquidity near the 1.00 peg while handling asymmetric run risk during depeg shocks.

---

## 3. Directory Layout
* `materials/` — Slide decks, syllabus PDFs, past questions.
* `notes/` — FX parity formulas, BOP models, currency risk notes.
* `primitives/` — Cross-currency swap invariant contracts and funding rate simulation scripts.

