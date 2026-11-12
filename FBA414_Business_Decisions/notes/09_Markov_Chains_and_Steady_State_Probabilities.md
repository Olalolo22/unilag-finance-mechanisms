# FBA 414: Note 09 — Markov Chains: Transition Matrices & Steady-State Analysis
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 21)  
**Exam Focus:** Transition Probability Matrices, Multi-Period Tree Diagrams, Chapman-Kolmogorov Equations, Long-Run Steady-State Equilibrium.

---

## 1. The Core Intuition
A **Markov Process** (named after Russian mathematician Andrey Markov) models dynamic systems that transition between finite states over discrete time steps.

The defining condition is the **Markovian Property (Memorylessness)**:
> *The probability of the system transitioning to any future state at time $t+1$ depends SOLELY on its current state at time $t$, and is completely independent of the past sequence of states that led to it.*

In business decision analysis, Markov analysis is extensively applied to:
1. **Brand Switching / Market Share Dynamics:** Customer loyalty vs. migration between competing telecom networks, banks, or FMCG brands.
2. **Credit Risk / Debt Ageing:** Accounts receivable transitioning from *Current* to *30-Days Overdue*, *60-Days Overdue*, and *Bad Debt Default*.
3. **Machine Maintenance:** Equipment transitioning from *Operational* to *Degraded* to *Breakdown*.

---

## 2. The Step-by-Step Algorithm ("The Recipe")

### Step 1: Define States & Construct the Transition Matrix (`P`)
* Identify all mutually exclusive and collectively exhaustive states: $S_1, S_2, \dots, S_k$.
* Construct the **Transition Probability Matrix (`P`)**:
  * Rows represent the **current state** at time $t$.
  * Columns represent the **next state** at time $t+1$.
  * `p_ij` = Probability that an entity currently in State $i$ moves to State $j$ in the next period.
* **CRITICAL INVARIANT:** Every row in matrix `P` must sum to exactly **`1.0`**:
  `SUM [ p_ij ] = 1.0` (for all $i$).

```text
               Next State (t+1)
               State 1   State 2
Current   S_1 [  p_11      p_12  ]   (p_11 + p_12 = 1.0)
State (t) S_2 [  p_21      p_22  ]   (p_21 + p_22 = 1.0)
```

---

### Step 2: Multi-Period State Predictions
Let the initial market share (or state distribution) at time $t=0$ be the row vector:
`pi^(0) = [ pi_1^(0),  pi_2^(0) ]`  *(where `pi_1 + pi_2 = 1.0`)*

* **State Distribution after 1 Period (`t=1`):**
  `pi^(1) = pi^(0) * P`
* **State Distribution after 2 Periods (`t=2`):**
  `pi^(2) = pi^(1) * P = pi^(0) * P^2`
* **State Distribution after $n$ Periods:**
  `pi^(n) = pi^(0) * P^n` (Chapman-Kolmogorov Equations).

---

### Step 3: Long-Run Steady-State Equilibrium Analysis
As time progresses ($n \to \infty$), many systems reach a **stationary equilibrium** where the proportion of entities in each state stabilizes and remains constant from period to period, regardless of the initial starting market shares.

Let `pi = [ pi_1, pi_2 ]` be the long-run steady-state vector.  
At equilibrium, transitioning for another period leaves the shares unchanged:
`pi * P = pi`

#### The 3-Step Solution Procedure for Steady-State:
1. Expand the vector-matrix multiplication `[ pi_1,  pi_2 ] * P = [ pi_1,  pi_2 ]` into a system of equations:
   * Equation 1: `pi_1 * p_11 + pi_2 * p_21 = pi_1`
   * Equation 2: `pi_1 * p_12 + pi_2 * p_22 = pi_2`
2. **The Redundancy Rule:** Equations 1 and 2 are mathematically dependent (redundant). **Discard either Equation 1 or Equation 2**.
3. **Substitute the Normalization Constraint:**
   `pi_1 + pi_2 = 1.0`  ===>  `pi_2 = 1.0 - pi_1`
4. Solve simultaneously for `pi_1` and `pi_2`.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> In the Nigerian retail banking sector, a survey examines customer account migration between two major banks: **Guaranty Trust Bank (GTBank)** and **Access Bank**.  
> The monthly customer retention and switching data reveals:
> * An existing GTBank customer has an **80% chance** of remaining with GTBank next month, and a **20% chance** of switching to Access Bank.
> * An existing Access Bank customer has a **70% chance** of remaining with Access Bank next month, and a **30% chance** of switching to GTBank.
> * Currently, GTBank holds **60%** of the market and Access Bank holds **40%**.
> 
> **Required:**  
> (a) Construct the Transition Probability Matrix.  
> (b) Calculate the expected market share for both banks after **1 month** and **2 months**.  
> (c) Determine the **long-run steady-state market share** for both banks.

---

### Step 1: Transition Probability Matrix (`P`)

Let State 1 = GTBank (G), State 2 = Access Bank (A).
* Row 1 (GTBank): Retention = `0.80`, Switch to Access = `0.20`. (Sum = 1.0)
* Row 2 (Access): Switch to GTBank = `0.30`, Retention = `0.70`. (Sum = 1.0)

```text
                  Next Month
               GTBank   Access Bank
Current  GTBank [ 0.80       0.20   ]
Month    Access [ 0.30       0.70   ]
```

Initial State Vector: `pi^(0) = [ 0.60,  0.40 ]`.

---

### Step 2: Market Shares after 1 Month (`pi^(1)`)

`pi^(1) = pi^(0) * P`
* `pi_GT^(1) = (0.60 * 0.80) + (0.40 * 0.30) = 0.48 + 0.12 = 0.60 (60%)`
* `pi_Access^(1) = (0.60 * 0.20) + (0.40 * 0.70) = 0.12 + 0.28 = 0.40 (40%)`

*Notice:* After 1 month, market shares remain at `60%` and `40%`! Let's check month 2.

---

### Step 3: Market Shares after 2 Months (`pi^(2)`)

`pi^(2) = pi^(1) * P`
* `pi_GT^(2) = (0.60 * 0.80) + (0.40 * 0.30) = 0.48 + 0.12 = 0.60 (60%)`
* `pi_Access^(2) = (0.60 * 0.20) + (0.40 * 0.70) = 0.12 + 0.28 = 0.40 (40%)`

---

### Step 4: Long-Run Steady-State Calculation

Let `pi = [ pi_1,  pi_2 ]` be the steady-state vector:
`[ pi_1,  pi_2 ] * [ [ 0.80, 0.20 ], [ 0.30, 0.70 ] ] = [ pi_1,  pi_2 ]`

#### Form Equations:
1. `0.80 * pi_1 + 0.30 * pi_2 = pi_1`
2. `0.20 * pi_1 + 0.70 * pi_2 = pi_2`
3. `pi_1 + pi_2 = 1.0`

Take Equation 1:
```text
0.80 * pi_1 + 0.30 * pi_2 = pi_1
0.30 * pi_2 = pi_1 - 0.80 * pi_1
0.30 * pi_2 = 0.20 * pi_1
pi_2 = (0.20 / 0.30) * pi_1 = (2 / 3) * pi_1
```

Substitute `pi_2 = (2/3) * pi_1` into the normalization constraint `pi_1 + pi_2 = 1.0`:
```text
pi_1 + (2 / 3) * pi_1 = 1.0
(5 / 3) * pi_1 = 1.0
pi_1 = 3 / 5 = 0.60 (60%)
```

Now solve for `pi_2`:
```text
pi_2 = 1.0 - pi_1 = 1.0 - 0.60 = 0.40 (40%)
```

---

### Step 5: Interpretation
* **Steady-State Market Share:**
  * **GTBank:** `60%`
  * **Access Bank:** `40%`
* **Managerial Takeaway:** The initial market shares of 60% and 40% were already at the steady-state equilibrium! The inflow of switching customers from Access to GTBank (`0.40 * 0.30 = 0.12`) exactly equals the outflow of switching customers from GTBank to Access (`0.60 * 0.20 = 0.12`).

---

## 4. Exam Traps & Gotchas

1. **The Row-Column Transposition Trap:**
   * Students often set up transition matrices with columns representing the current state and rows representing the next state.
   * **Rule:** In UNILAG exams, **ROWS = Current State (at $t$)** and **COLUMNS = Next State (at $t+1$)**. Every row **must sum to 1.0**. If your rows don't sum to 1.0, your matrix is inverted!
2. **Forgetting to Discard a Dependent Equation:**
   * If you try to solve Equation 1 and Equation 2 simultaneously without the constraint `pi_1 + pi_2 = 1`, you will get `0 = 0` (infinitely many solutions). You **must** discard one equation and replace it with `pi_1 + pi_2 = 1`.
3. **Absorbing States:**
   * An **absorbing state** is a state that, once entered, cannot be left (e.g. `p_ii = 1.0`).
   * If a system has absorbing states (like bankruptcy or terminal death), the long-run probability of being in any non-absorbing (transient) state is **zero**.
