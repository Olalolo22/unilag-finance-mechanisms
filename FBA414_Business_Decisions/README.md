# FBA 414: Analysis for Business Decisions

**Department:** Management Sciences / Finance | **Units:** 2 | **Exam Mode:** CBT (Computer-Based Test)

---

## 1. Course Overview & Core Topics
FBA 414 focuses on quantitative modeling and operational research for executive decision-making:
* **Decision Theory Under Uncertainty:** Maximin, Maximax, Laplace, Hurwicz criterion, and Minimax Regret.
* **Decision Trees & Expected Monetary Value (EMV):** Sequential decision nodes, chance nodes, rollback method, Expected Value of Perfect Information (EVPI).
* **Linear Programming & Optimization:** Graphical method, Simplex method, sensitivity analysis, shadow prices, dual problems.
* **Forecasting & Time Series Analysis:** Moving averages, exponential smoothing, trend projection, regression models.
* **Inventory Control Models:** Economic Order Quantity (EOQ), reorder points, safety stock, carrying costs vs ordering costs.

---

## 2. The On-Chain Mechanism Analogue

### A. Decision Trees & Solver Routing Under Latency
* **TradFi:** `EMV = Sum(Probability_i * Payoff_i)`
* **Protocol Analogue:** Intent clearing and solver auctions (e.g. UniswapX / CoW Swap / RouteDock). Solvers model the probability of execution, gas cost volatility, and slippage to find the optimal trade route across fragmented liquidity pools.

### B. Linear Programming, Shadow Prices & AMM Dynamic Fees
* **TradFi:** Optimization subject to constraints `Ax <= b`. The "shadow price" is the marginal value of relaxing a constrained resource by one unit.
* **Protocol Analogue:** Uniswap v4 dynamic fee hooks. When liquidity at a tick becomes constrained or volatility surges, the marginal fee must increase to compensate LPs for Adverse Selection / Loss-Versus-Rebalancing (LVR).

### C. EOQ & Gas-Optimal Batching
* **TradFi:** `EOQ = sqrt((2 * Demand * Setup_Cost) / Holding_Cost)`
* **Protocol Analogue:** Rollup batching and keeper execution intervals. Balancing fixed L1 state posting costs (setup cost) against user wait-time / latency risk (holding cost).

---

## 3. Directory Layout
* `materials/` — Slide decks, CBT past questions.
* `notes/` — Decision trees, LP formulation guides, inventory math.
* `primitives/` — Solver routing algorithms and keeper batching scripts.

