# FIN 433 / FIN 412: Lecture 2 — Capital Structure & Firm Value
**Lecturer:** Dr. Peter N. Amah, Department of Finance, University of Lagos  

---

## 1. Foundational Definitions
* **Capital Structure:** The composition of long-term permanent sources of funds used to finance a firm (Equity, Debt, and Preference capital).
* **Financial Structure:** Includes all sources of financing—both short-term (bank overdrafts, accounts payable, short-term loans) and long-term capital.
* **Optimal Capital Structure:** The target debt-equity mix that **minimizes WACC (Kw)** and **maximizes total market value of the firm (MV)**.

---

## 2. Competing Theories of Capital Structure

### Summary Comparison Table
| Feature | Net Income Theory (NIT) | Net Operating Income (NOIT) | Trade-Off Theory (TOT) | M&M (No Taxes, 1958) | M&M (With Taxes, 1963) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Does Leverage Matter?** | YES | NO | YES | NO | YES |
| **Cost of Debt (Kd)** | Constant | Constant | Constant then rises | Constant | Constant |
| **Cost of Equity (Ke)** | Constant | Linear increasing function | Upward curving | Linear increasing function | Linear increasing function |
| **WACC (Kw)** | Declines continuously | Constant | U-shaped (minimum at L*) | Constant | Declines continuously |
| **Optimal Leverage** | 100% Debt | None (Indifferent) | Point L* (Tax shield vs bankruptcy) | None (Indifferent) | 100% Debt |

---

## 3. Net Income Theory (NIT)
* **Pillars:**
  1. `Kd` is lower than `Ke` and unaffected by leverage.
  2. `Ke` does not increase with leverage (shareholders ignore financial risk).
  3. Increasing cheap debt continuously drives down WACC (`Kw`).
* **Formulae:**
  * `E = (NOI - Int) / Ke`
  * `MV = E + D = NOI / Kw`
  * `Kw = (E / MV) * Ke + (D / MV) * Kd`

---

## 4. Net Operating Income Theory (NOIT)
* **Pillars:**
  1. Total market value `MV` is determined by capitalizing Net Operating Income (`NOI` or `EBIT`) at the constant overall cost of capital `Kw`:
     `MV = NOI / Kw`
  2. `Kw` and `Kd` are completely invariant to leverage.
  3. Cost of equity `Ke` increases linearly to offset the financial risk of debt:
     `Ke = Kw + (Kw - Kd) * (D / E)`

---

## 5. Traditional / Trade-Off Theory (TOT / Static Theory)
* **Pillars:**
  * Between `0` and `L*`: Cost of debt is low, risk of default is negligible. Debt lowers WACC and increases firm value (agrees with NIT).
  * At `L*` (**Optimal Leverage**): Marginal present value of interest tax shields equals the marginal present value of financial distress/bankruptcy costs. WACC is minimized, firm value is maximized.
  * Beyond `L*`: Excessive debt raises default risk. Both `Kd` and `Ke` spike sharply, driving WACC up and destroying firm value.

---

## 6. Miller & Modigliani (M&M) Without Taxes (1958)
* **Core Thesis:** Firm value is independent of capital structure. "The size of the pie does not depend on how it is sliced."
* **M&M Assumptions:**
  1. Homogeneous risk classes across firms.
  2. Perfect capital markets (no transaction costs, free information).
  3. Individuals and corporations can borrow and lend at the same risk-free rate.
  4. No corporate or personal taxes.
  5. No bankruptcy or agency costs.
  6. Perpetual operating cash flows.

### Proposition I:
`V_L = V_U = NOI / Kw`
The market value of any firm is independent of its capital structure.

### Proposition II (Derivation):
Start from WACC definition:
`Kw = Ke * (E / (D + E)) + Kd * (D / (D + E))`
`Kw * (D + E) = Ke * E + Kd * D`
`Kw * D + Kw * E = Ke * E + Kd * D`
`(Kw - Kd) * D = (Ke - Kw) * E`
`Ke - Kw = (Kw - Kd) * (D / E)`
`Ke = Kw + (Kw - Kd) * (D / E)`

### The Proofs of M&M Irrelevance:
1. **Home-Made Leverage (HML):** Individual investors can borrow on personal account to replicate the exact returns and risk of a levered firm. Therefore, investors will not pay a premium for corporate leverage.
2. **The Arbitrage Process:** If a levered firm (`V_L`) trades at a higher valuation than an identical unlevered firm (`V_U`), arbitrageurs sell their overvalued levered shares, borrow on personal account, and buy undervalued unlevered shares. The selling pressure on `V_L` and buying pressure on `V_U` restores equilibrium instantaneously.

---

## 7. M&M With Corporate Taxes (1963)
When interest expense is tax-deductible, debt provides an annual tax shield of `Tc * (Kd * D)`. Since debt is perpetual, the present value of the tax shield is:
`PV(Tax Shield) = (Tc * Kd * D) / Kd = Tc * D`

### Proposition I (With Tax):
`V_L = V_U + Tc * D`
Where:
`V_U = EBIT * (1 - Tc) / Ku`
* `Ku` = Unlevered cost of equity.

### Proposition II (With Tax):
`Ke = Ku + (Ku - Kd) * (D / E) * (1 - Tc)`

### WACC Formula (With Tax):
`Kw = Ke * (E / (D + E)) + Kd * (D / (D + E)) * (1 - Tc)`
