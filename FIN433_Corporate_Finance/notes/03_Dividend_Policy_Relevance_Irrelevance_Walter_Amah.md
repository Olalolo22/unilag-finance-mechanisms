# FIN 433 / FIN 412: Lecture 3 — Dividend Policy Decisions
**Lecturer:** Dr. Peter N. Amah, Department of Finance, University of Lagos  

---

## 1. Key Concepts, Corporate Dates & Dividend Types

### Key Corporate Dates (Chronological Order):
1. **Declaration Date:** The board of directors passes a formal resolution proposing dividend payout.
2. **Ex-Dividend Date:** The cutoff date (usually 2 business days before record date). Buyers purchasing on or after this date do NOT receive the declared dividend. Stock price drops by approximately the dividend amount.
3. **Date of Record:** The date the registrar closes books to determine registered shareholders entitled to payment.
4. **Payment Date:** Dividend warrants/electronic transfers are dispatched to shareholders of record.

### Types of Dividend:
* **Cash Dividends:** Regular cash, special/extra cash, liquidating cash dividends.
* **Scrip / Bonus Dividend (Stock Dividend):** Additional shares issued pro-rata to existing shareholders.
  * *Effect:* Total share count increases, nominal price per share unchanged, reserves decrease, but **total firm book value and market capitalization remain unchanged**. Market price per share adjusts downwards:
    `P_ma = (N_b * P_mb) / N_a`
* **Stock Split:** Existing shares are divided into a higher quantity of lower par value shares (e.g., 2:1 split).
  * *Effect:* Share count doubles, par value halves, reserves unchanged, **total firm value remains identical**.
* **Share Repurchases (Buybacks):** Firm buys its own shares back from the open market.
  * *Effect:* Reduces cash, reduces shares outstanding, increases EPS/ROE, but firm value remains governed by operating cash flows.

---

## 2. Schools of Thought on Dividend Policy

```text
┌──────────────────────────────────────┐     ┌──────────────────────────────────────┐
│     TRADITIONAL RIGHT (Relevance)    │     │       RADICAL LEFT (Relevance)       │
├──────────────────────────────────────┤     ├──────────────────────────────────────┤
│ • High payout = High market value    │     │ • Low payout / High retention = High │
│ • "Bird-in-the-Hand" argument        │     │   market value                       │
│ • Current dividend is less risky     │     │ • True for growth firms (k > Ke)     │
│   than uncertain future capital gain │     │ • Capital gains tax advantages       │
└──────────────────────────────────────┘     └──────────────────────────────────────┘
                                  │
                                  ▼
               ┌──────────────────────────────────────┐
               │    MILLER & MODIGLIANI (1961)        │
               │        (Dividend Irrelevance)        │
               ├──────────────────────────────────────┤
               │ • Dividend policy does NOT matter    │
               │ • Firm value depends on earning power│
               │   and investment policy, not payout  │
               └──────────────────────────────────────┘
```

---

## 3. The Miller & Modigliani (M&M) Dividend Irrelevance Proof (1961)

M&M proved mathematically that dividend payout cancels out of the firm valuation equation:

1. **Single Period Valuation:**
   `P_0 = (D_1 + P_1) / (1 + R_1)`
2. **Total Equity Value with `n_0` shares:**
   `n_0 * P_0 = (n_0 * D_1 + n_0 * P_1) / (1 + R_1)`
3. **Financing New Investment `I_1`:**
   New investments can only be funded by Net Operating Cash Flow (`NOC_1`) or issuing `m_1` new shares at price `P_1`:
   `NOC_1 + m_1 * P_1 = I_1 + n_1 * D_1`
   `m_1 * P_1 = -NOC_1 + I_1 + n_1 * D_1`
4. **Total Shares at Period 1:**
   `n_1 = n_0 + m_1  =>  n_0 = n_1 - m_1`
5. **Substituting into the Valuation Equation:**
   `n_0 * P_0 = [n_1 * D_1 + n_1 * P_1 - m_1 * P_1] / (1 + R_1)`
   `n_0 * P_0 = [n_1 * D_1 + n_1 * P_1 - (-NOC_1 + I_1 + n_1 * D_1)] / (1 + R_1)`
   `n_0 * P_0 = [n_1 * P_1 + NOC_1 - I_1] / (1 + R_1)`

**Crucial Exam Takeaway:**
> **Dividend (`D_1`) has been completely eliminated from the valuation equation.** 
> The current market value of the firm depends purely on future terminal value (`n_1 * P_1`), net operating cash flow (`NOC_1`), and new investment (`I_1`), **NOT on dividend payout.**

---

## 4. Walter's Hybrid Model

Professor James E. Walter proposed that dividend policy relevance depends on the relationship between the firm's internal rate of return (`k` or `r`) and its cost of equity capital (`Ke`):

### Formula:
`P_0 = [D_1 + (k / Ke) * (E_1 - D_1)] / Ke`
Where:
* `P_0` = Market price per share
* `D_1` = Dividend per share
* `E_1` = Earnings per share (EPS)
* `(E_1 - D_1)` = Retained earnings per share
* `k` = Firm's internal rate of return on investment
* `Ke` = Market capitalization rate / cost of equity

### The Three Scenarios:
1. **Growth Firms (`k > Ke`):**
   * The firm earns higher returns on retained earnings than shareholders could earn elsewhere.
   * **Optimal Dividend Payout = 0% (100% Retention).**
   * Retaining earnings maximizes shareholder wealth (supports Radical Left).
2. **Declining Firms (`k < Ke`):**
   * The firm earns lower returns on projects than the market rate.
   * **Optimal Dividend Payout = 100% (0% Retention).**
   * Paying out all earnings maximizes shareholder wealth (supports Traditional Right).
3. **Normal / Mature Firms (`k = Ke`):**
   * The firm earns exactly the market return.
   * **Dividend policy is completely irrelevant.** Firm value remains unchanged regardless of payout ratio (agrees with M&M).

