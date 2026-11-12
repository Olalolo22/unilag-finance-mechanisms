# FIN 433: Theory of Corporate Finance ("The Olowe Era")

**Department:** Finance | **Units:** 3 | **Exam Mode:** Written (Theory & Quantitative)

---

## 1. Course Overview & Core TradFi Topics
FIN 433 is the premier theoretical corporate finance course at UNILAG. It covers:
* **Capital Structure Theory:** Modigliani-Miller Theorems (Proposition I & II with and without corporate taxes), Trade-off Theory (tax shields vs financial distress costs), Pecking Order Theory.
* **Dividend Policy:** Walter's Model, Gordon's Growth Model, Modigliani-Miller Dividend Irrelevance hypothesis, Client effect.
* **Utility Theory & Choice Under Uncertainty:** Expected utility, risk aversion (concave utility curves), Arrow-Pratt measures of risk aversion, certainty equivalents.
* **Capital Investment Analysis (Real Options):** Capital budgeting under uncertainty, net present value (NPV) vs internal rate of return (IRR), option to expand, delay, or abandon.
* **Capital Markets Efficiency:** Weak, semi-strong, and strong form market efficiency.

---

## 2. The On-Chain Mechanism Analogue

### A. Modigliani-Miller & Protocol Capital Structure
* **TradFi:** `V_L = V_U + (T_C * D) - PV(Financial Distress)`
  * `V_L` = Value of leveraged firm
  * `V_U` = Value of unleveraged firm
  * `T_C` = Corporate tax rate
  * `D` = Debt issued
* **Protocol Analogue:** How a protocol balances debt-like obligations (minted stablecoins or CDPs like MakerDAO DAI / Liquity LUSD) against governance token equity (MKR / LQTY). When debt expands too rapidly without adequate liquidation buffers, financial distress (bad debt cascades) destroys the protocol's equity value.

### B. Utility Theory & Liquidation Bonus Curves
* **TradFi:** Investors require a risk premium proportional to their degree of risk aversion `A = -U''(W) / U'(W)` to hold uncertain payoffs.
* **Protocol Analogue:** Liquidator incentives in lending markets (Aave / Compound / Morpho). Liquidators take inventory risk when seizing volatile collateral. The protocol must calibrate the liquidation bonus (e.g. 5% to 10%) so that liquidators have positive expected utility after factoring in gas fees, slippage on DEX AMMs, and execution latency.

### C. Real Options & Structured Covered-Call Vaults (*Harvest* / *SOLO*)
* **TradFi:** Black-Scholes and piecewise payoff structuring:
  `Payoff = S_T - max(0, S_T - K) = min(S_T, K)`
* **Protocol Analogue:** Covered-call vaults on tokenized equities (*Harvest* on Backed Finance xStocks). Selling the right to upside beyond strike `K` to lock in upfront yield premium for tokenized equity holders.

---

## 3. Directory Layout
* `materials/` — Slide decks, syllabus PDFs, past questions.
* `notes/` — Chapter summaries (Capital Structure, Dividends, Utility).
* `primitives/` — Smart contract implementations of payoff curves and auction incentive models.

