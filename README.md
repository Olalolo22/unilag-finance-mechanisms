# UNILAG Year 4 Finance Curriculum → On-Chain Protocol Architecture

This repository houses course notes, syllabus breakdowns, and systematic mechanism design mappings for the final-year (400 Level) Finance curriculum at the University of Lagos (UNILAG).

Rather than treating academic coursework as separate from protocol engineering, this repository maps classical financial economics and corporate finance directly to decentralized state machines, AMM microstructure, and tokenized primitives.

---

## Course Structure & Mechanism Mapping

| Course Code | Title | Core TradFi Topics | On-Chain / Mechanism Analogue |
| :--- | :--- | :--- | :--- |
| **[FIN 433](./FIN433_Corporate_Finance/)** | Theory of Corporate Finance (*"The Olowe Era"*) | Capital Structure (Modigliani-Miller), Dividend Policy, Utility Theory, Real Options, Capital Markets | CDP Debt vs Equity tokens (MakerDAO), Liquidation bonus curves, Structured covered-call vaults (*Harvest* / *SOLO*). |
| **[FIN 418](./FIN418_International_Finance/)** | International Business Finance | FX Rate Determination, Covered/Uncovered Interest Rate Parity (CIRP/UIRP), Balance of Payments, Currency Hedging | Cross-currency AMM invariant curves, Stablecoin peg/arbitrage loops, Cross-chain bridge liquidity imbalances, Perpetual funding rates. |
| **[FIN 417](./FIN417_Bank_Lending/)** | Bank Lending & Loan Administration | The 6 Cs of Credit, Collateral Haircuts, Loan Administration, Default Workouts & Case Studies | Decentralized lending engines (Aave, Morpho), LTV & Liquidation thresholds, Bad debt socialization, Pre-trade risk firewalls (*RogueTrader*). |
| **[FBA 414](./FBA414_Business_Decisions/)** | Analysis for Business Decisions | Quantitative Decision Models, Decision Trees, Payoff Matrices, Optimization, Linear Programming | Game-theoretic mechanism design, Solver routing, MEV searcher payoffs, Dynamic AMM fees (Uniswap v4 hooks). |
| **[FBA 411](./FBA411_Strategic_Management/)** | Business Policy & Strategic Management | Corporate Strategy, Competitive Positioning, Organizational Policies, Switching Costs | Protocol moats, Vampire attack defense, Liquidity retention mechanisms, Token governance design. |

---

## Folder Organization

Each course folder contains:
1. `README.md` — Detailed syllabus breakdown, key theoretical formulas, and the 1-to-1 mechanism translation.
2. `notes/` — Chapter summaries and lecture notes.
3. `materials/` — Dedicated folder for slides, past questions, and reading PDFs from Google Drive.
4. `primitives/` — Code prototypes (Solidity / Rust / TypeScript) implementing the course's economic formulas on-chain.
