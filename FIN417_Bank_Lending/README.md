# FIN 417: Bank Lending & Loan Administration

**Department:** Finance | **Units:** 3 | **Exam Mode:** Written (Theory & Case Studies)

---

## 1. Course Overview & Core TradFi Topics
FIN 417 covers the operational, regulatory, and credit assessment framework of commercial lending:
* **The 6 Cs of Credit:** Character, Capacity, Capital, Collateral, Conditions, and Common Sense.
* **Types of Collateral & Securities:** Mortgages, pledges, hypothecation, liens, guarantees, and debentures. Perfecting security interests.
* **Credit Analysis & Underwriting:** Cash flow evaluation, Debt Service Coverage Ratio (DSCR), Loan-to-Value (LTV) limits, Interest Coverage Ratio.
* **Loan Administration & Monitoring:** Covenant enforcement (affirmative and negative covenants), loan documentation, disbursement controls.
* **Non-Performing Loans (NPLs) & Workouts:** Early warning signals, restructuring, loan provisioning, asset recovery, and liquidation.

---

## 2. The On-Chain Mechanism Analogue

### A. Collateral Haircuts, LTV & Liquidation Thresholds
* **TradFi:** `Max Loan Amount = Market Value of Collateral * (1 - Haircut)`
  * Bank demands a 30% haircut on real estate (LTV = 70%) to protect against market price declines.
* **Protocol Analogue:** Aave / Morpho / Compound risk parameters.
  * Maximum LTV (e.g. 75% for ETH, 50% for volatile tokens).
  * Liquidation Threshold (e.g. 80% where account becomes undercollateralized).
  * The difference (`Liquidation Threshold - Max LTV`) is the safety buffer protecting protocol solvency against oracle latency and price slippage.

### B. Pre-Trade Risk Systems (PTRS) & Covenant Enforcement
* **TradFi:** Negative covenants prevent a borrower from taking on junior debt or depleting cash reserves without bank approval.
* **Protocol Analogue:** Pre-Trade Risk Systems (PTRS) like *RogueTrader*. A deterministic smart contract firewall enforcing balance limits, maximum leverage ceilings, and stop-loss bounds *before* execution commits to prevent cascading liquidations.

### C. NPL Workouts & Bad Debt Socialization
* **TradFi:** When a borrower defaults and collateral auction fails to cover the loan balance, the bank writes off bad debt against loan loss reserves.
* **Protocol Analogue:** Protocol insolvency handling. When rapid liquidation cascades cause bad debt (e.g. liquidated collateral sells for less than borrowed amount), protocols use backstop safety modules (slashing staked tokens, insurance pools, or auctioning newly minted governance tokens).

---

## 3. Directory Layout
* `materials/` — Slide decks, case studies, past questions.
* `notes/` — Credit scoring models, collateral law, loan covenant notes.
* `primitives/` — Liquidation engine simulation contracts and health factor monitoring bots.
