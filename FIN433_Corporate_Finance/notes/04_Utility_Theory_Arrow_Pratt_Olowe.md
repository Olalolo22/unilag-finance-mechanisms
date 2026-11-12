# FIN 412 / FIN 433: Utility Theory & Choice Under Uncertainty
**Lecturer:** Prof. R. A. Olowe  
**Recommended Texts:**  
- Olowe, R. A. (2017). *Financial Management: Concepts, Financial System and Business Finance* (4th ed.). Lagos: Brierly Jones (ORA).  
- Copeland, T. E., & Weston, J. F. (1983). *Financial Theory and Corporate Policy* (Chap. 3).  

---

## 1. Overview & Foundational Concepts
* **Definition:** Utility theory is the normative theory of choice by rational individuals when faced with risky (uncertain) alternatives.
* **Core Goal:** An individual does not merely maximize expected monetary value; they make choices among risky alternatives in such a way as to obtain **maximum expected utility (satisfaction)**.
* **Measurement:** The unit of measurement of cardinal utility is called **utiles**.
* **Cardinal vs. Ordinal Utility:**
  * *Ordinal Utility:* Ranks preferences (e.g., A is preferred to B, but cannot quantify the degree of preference).
  * *Cardinal Utility:* Assigns measurable numerical values to satisfaction, allowing expected utilities of gambles to be calculated, weighted by probabilities, and compared.

---

## 2. The 5 Axioms of Cardinal Utility (Von Neumann-Morgenstern / Copeland & Weston)
To construct a consistent cardinal utility function, an individual's behavior must satisfy five foundational axioms:

### Axiom 1: Comparability (Completeness)
* For an entire set `S` of uncertain alternatives, an individual can specify preferences between any pair of outcomes `x` and `y`:
  * Either `x` is strictly preferred to `y` (`x > y`),
  * Or `y` is strictly preferred to `x` (`y > x`),
  * Or the individual is indifferent between `x` and `y` (`x ~ y`).
* No undefined or incomparable choices exist.

### Axiom 2: Transitivity (Consistency)
* Individual choices must be logically consistent:
  * If outcome `x` is indifferent to `y` (`x ~ y`) and `y` is indifferent to `z` (`y ~ z`), then outcome `x` must be indifferent to `z` (`x ~ z`).
  * Similarly, if `x > y` and `y > z`, then `x > z`.

### Axiom 3: Strong Independence
* Suppose a gamble `G(x, z: alpha)` gives outcome `x` with probability `alpha` and outcome `z` with probability `(1 - alpha)`.
* If an individual is indifferent between outcome `x` and outcome `y` (`x ~ y`), then substituting `y` for `x` does not alter preference:
  `G(x, z: alpha) ~ G(y, z: alpha)`
* The preference between `x` and `y` is independent of the third outcome `z`.

### Axiom 4: Measurability
* If an individual ranks outcomes such that `x > y >= z` or `x >= y > z`, there exists a unique probability `alpha` (`0 < alpha < 1`) such that the individual is indifferent between receiving outcome `y` with certainty and facing a gamble between `x` and `z`:
  `y ~ G(x, z: alpha)`
* This axiom establishes that utilities can be quantified on an interval scale.

### Axiom 5: Ranking
* If two intermediate outcomes `y` and `u` lie between `x` and `z` (i.e., `x >= y >= z` and `x >= u >= z`), we can establish unique gambles such that:
  `y ~ G(x, z: alpha_1)` and `u ~ G(x, z: alpha_2)`
* It follows directly that:
  * If `alpha_1 > alpha_2`, then outcome `y` is strictly preferred to outcome `u` (`y > u`).
  * If `alpha_1 = alpha_2`, then the individual is indifferent between `y` and `u` (`y ~ u`).

---

## 3. Extension & The Theory of Choice
1. **The Greed Assumption (Non-Satiation):**
   * Investors always prefer more wealth to less. Mathematically, the first derivative of the utility function with respect to wealth is strictly positive:
     `U'(w) = dU(w) / dw > 0` (Positive Marginal Utility of Wealth).
2. **The Principle of Maximizing Expected Utility:**
   * Given the five axioms plus non-satiation, a rational decision-maker will always seek to **maximize their expected utility of wealth**, `E[U(w)]`, rather than nominal expected wealth `E(w)`.
   * When evaluating alternatives, the individual calculates `E[U(w)]` for every option and selects the outcome that maximizes expected utility.

### Key Distinction: Expected Wealth vs. Expected Utility
For a gamble with `n` possible wealth outcomes `w_i`, each occurring with probability `P_i`:
* **Expected Wealth:**
  `E(w) = SUM [ P_i * w_i ]`
* **Expected Utility:**
  `E[U(w)] = SUM [ P_i * U(w_i) ]`
* **Utility of Expected Wealth:**
  `U[E(w)] = U( SUM [ P_i * w_i ] )`

---

## 4. Shapes & Functional Forms of Utility Functions
Utility functions are plotted with Wealth (`w`) on the horizontal axis and Utility of Wealth (`U(w)`) on the vertical axis. Common algebraic forms include:

1. **Linear Function:**
   `U(w) = a + b * w` (where `b > 0`)
   * First derivative: `U'(w) = b` (constant marginal utility).
   * Second derivative: `U''(w) = 0`.
   * Characterizes **Risk Neutrality**.

2. **Quadratic Function:**
   `U(w) = a + b * w - c * w^2` (where `b > 0, c > 0`)
   * First derivative: `U'(w) = b - 2*c*w` (positive only when `w < b / (2*c)`).
   * Second derivative: `U''(w) = -2*c < 0`.
   * Characterizes **Risk Aversion**, but has the unrealistic economic property of increasing absolute risk aversion with wealth.

3. **Cubic Function:**
   `U(w) = a + b * w + c * w^2 + d * w^3`

4. **Logarithmic Function:**
   `U(w) = ln(w)` (for `w > 0`)
   * First derivative: `U'(w) = 1 / w > 0`.
   * Second derivative: `U''(w) = -1 / (w^2) < 0`.
   * Characterizes **Risk Aversion** with diminishing marginal utility and decreasing absolute risk aversion (standard benchmark in financial economics).

---

## 5. Attitudes Toward Risk
Given that marginal utility is positive (`U'(w) > 0`), the curvature of the utility function (sign of `U''(w)`) reveals an investor's attitude toward risk:

| Attitude to Risk | Curvature of `U(w)` | Second Derivative | Comparison Condition | Economic Meaning |
| :--- | :--- | :--- | :--- | :--- |
| **Risk Averse** | Strictly **Concave** | `U''(w) < 0` | `U[E(w)] > E[U(w)]` | Prefers expected wealth with certainty over taking the gamble. |
| **Risk Neutral** | **Linear** | `U''(w) = 0` | `U[E(w)] = E[U(w)]` | Indifferent between a certain outcome and a gamble with equal expected value. |
| **Risk Lover** | Strictly **Convex** | `U''(w) > 0` | `U[E(w)] < E[U(w)]` | Prefers taking the gamble over receiving expected wealth with certainty. |

---

## 6. Certainty Equivalent Wealth, Risk Premium & Cost of Gamble

### 1. Certainty Equivalent Wealth (CEW)
* **Definition:** The guaranteed cash amount that yields exactly the same level of utility as the uncertain gamble.
* **Equation:**
  `U(CEW) = E[U(w)]`
  `CEW = U_inverse( E[U(w)] )`
  * For logarithmic utility: If `ln(CEW) = E[U(w)]`, then `CEW = exp( E[U(w)] )`.

### 2. Risk Premium (`pi`)
* **Definition:** The maximum monetary amount an investor is willing to pay/sacrifice to eliminate risk and exchange an uncertain gamble for its Certainty Equivalent.
* **Formula:**
  `Risk Premium = Expected Wealth - Certainty Equivalent Wealth`
  `Risk Premium = E(w) - CEW`
* **Interpretation of Signs:**
  * For a **Risk Averse** investor: `E(w) > CEW` implies `Risk Premium > 0`.
  * For a **Risk Neutral** investor: `E(w) = CEW` implies `Risk Premium = 0`.
  * For a **Risk Lover**: `E(w) < CEW` implies `Risk Premium < 0`.

### 3. Cost of the Gamble
* **Formula:**
  `Cost of Gamble = Current Wealth (w_0) - CEW`

---

## 7. Step-by-Step Worked Example (Lecture Example 1)

### Problem Statement:
> Olu, with an initial wealth of N20,000, is faced with a gamble that has a 60% chance of winning N10,000 and a 40% chance of winning N500. Olu has a logarithmic utility function `U(w) = ln(w)`.  
> What is his attitude to risk? Calculate his Expected Wealth, Utility of Expected Wealth, Expected Utility, Certainty Equivalent Wealth, Risk Premium, and Cost of the Gamble.

### Step 1: Calculate Total Wealth Outcomes
* If Olu wins N10,000:
  `w_1 = 20,000 + 10,000 = N30,000` (Probability `P_1 = 0.60`)
* If Olu wins N500:
  `w_2 = 20,000 + 500 = N20,500` (Probability `P_2 = 0.40`)

### Step 2: Calculate Expected Wealth `E(w)`
`E(w) = (0.60 * 30,000) + (0.40 * 20,500)`  
`E(w) = 18,000 + 8,200 = N26,200`

### Step 3: Calculate Utility of Expected Wealth `U[E(w)]`
`U[E(w)] = ln(26,200) = 10.1735 utiles` (slide rounded: `10.17 utiles`)

### Step 4: Calculate Expected Utility of Gamble `E[U(w)]`
* `U(w_1) = ln(30,000) = 10.30898 utiles`
* `U(w_2) = ln(20,500) = 9.92818 utiles`
* `E[U(w)] = (0.60 * 10.30898) + (0.40 * 9.92818)`  
  `E[U(w)] = 6.18539 + 3.97127 = 10.15666 utiles` (slide rounded: `10.16 utiles`)

### Step 5: Determine Attitude to Risk
* Compare `U[E(w)]` with `E[U(w)]`:
  `U[E(w)] = 10.17 > E[U(w)] = 10.16`
* **Conclusion:** Since `U[E(w)] > E[U(w)]`, Olu is strictly **Risk Averse**.

### Step 6: Calculate Certainty Equivalent Wealth (CEW)
`U(CEW) = E[U(w)]`  
`ln(CEW) = 10.16 utiles`  
`CEW = exp(10.16) = N25,848.30`  
*(Note: Using exact unrounded 10.15666 utiles gives `exp(10.15666) = N25,762.66`).*

### Step 7: Calculate Risk Premium
`Risk Premium = E(w) - CEW`  
`Risk Premium = N26,200 - N25,848.30 = N351.70`

### Step 8: Calculate Cost of the Gamble
`Cost of Gamble = Current Wealth - CEW`  
`Cost of Gamble = N20,000 - N25,848.30 = -N5,848.30`  
*(A negative cost indicates that taking the gamble increases certainty-equivalent wealth by N5,848.30 above initial wealth).*

---

## 8. Arrow-Pratt Measures of Risk Aversion (Pratt 1964, Arrow 1971)

### Theoretical Background & Local Risk Premium Derivation
Consider an investor with wealth `w` offered an actuarially neutral gamble `Z` (where `E(Z) = 0` and variance is `sigma_z^2`).  
The risk premium `pi(w, Z)` satisfies:
`E[U(w + Z)] = U(w - pi)`

Using a Taylor series expansion of both sides around `w`:
* LHS: `E[U(w + Z)] approx = U(w) + U'(w)*E(Z) + (1/2)*U''(w)*E(Z^2) = U(w) + (1/2)*(sigma_z^2)*U''(w)`
* RHS: `U(w - pi) approx = U(w) - pi * U'(w)`

Equating LHS and RHS:
`U(w) + (1/2)*(sigma_z^2)*U''(w) = U(w) - pi * U'(w)`  
`(1/2)*(sigma_z^2)*U''(w) = -pi * U'(w)`  
`pi approx = (1/2) * (sigma_z^2) * [ -U''(w) / U'(w) ]`

Since variance `(1/2)*(sigma_z^2)` is always positive, the sign and magnitude of the risk premium are determined by the ratio in brackets: `[-U''(w) / U'(w)]`.

### 1. Absolute Risk Aversion (ARA)
Measures risk aversion for a given absolute dollar/Naira level of wealth:
`ARA = -U''(w) / U'(w)`

* **Application to Logarithmic Utility `U(w) = ln(w)`:**
  * `U'(w) = 1 / w`
  * `U''(w) = -1 / (w^2)`
  * `ARA = -(-1 / w^2) / (1 / w) = (1 / w^2) * (w / 1) = 1 / w`
* **Economic Property:** As wealth `w` increases, `ARA = 1/w` decreases. This is known as **Decreasing Absolute Risk Aversion (DARA)** — wealthier individuals are willing to hold more absolute Naira in risky assets.
* For Example 1 at `w = N20,000`:
  `ARA = 1 / 20,000 = 0.00005`

### 2. Relative Risk Aversion (RRA)
Measures risk aversion to proportional or percentage changes in wealth:
`RRA = w * ARA = -w * [ U''(w) / U'(w) ]`

* **Application to Logarithmic Utility `U(w) = ln(w)`:**
  `RRA = w * (1 / w) = 1`
* **Economic Property:** Since `RRA = 1` is constant for all wealth levels, logarithmic utility exhibits **Constant Relative Risk Aversion (CRRA)**.
* **Economic Meaning:** An individual with constant relative risk aversion will allocate a constant percentage of their portfolio to risky assets, regardless of changes in total wealth.

---

## 9. Comprehensive Solution to Slide 25 Review Question

### Question:
> Suppose an individual with a logarithmic utility function `U(w) = ln(w)` and an initial wealth of N5,000,000 is exposed to a situation that results in a 50/50 chance of winning or losing N1,000,000.  
> If the individual can buy insurance that completely removes the risk for a fee of N125,000, should he buy it or take the gamble?

---

### Method A: Comparing Expected Utility of Gamble vs. Utility with Insurance

#### 1. Analyze the Uncertain Gamble:
* Initial wealth: `w_0 = N5,000,000`
* State 1 (Win N1,000,000):
  * Total wealth: `w_win = 5,000,000 + 1,000,000 = N6,000,000`
  * Probability: `P_1 = 0.50`
  * Utility: `U(w_win) = ln(6,000,000) = 15.607270 utiles`
* State 2 (Lose N1,000,000):
  * Total wealth: `w_loss = 5,000,000 - 1,000,000 = N4,000,000`
  * Probability: `P_2 = 0.50`
  * Utility: `U(w_loss) = ln(4,000,000) = 15.201805 utiles`

* Expected Utility of taking the gamble `E[U(w)]`:
  `E[U(w)] = (0.50 * 15.607270) + (0.50 * 15.201805)`  
  `E[U(w)] = 7.803635 + 7.6009025 = 15.404538 utiles`

#### 2. Analyze the Insured Alternative:
* If the individual purchases insurance for an upfront fee of N125,000, risk is completely eliminated.
* Guaranteed wealth after paying insurance fee:
  `w_insured = 5,000,000 - 125,000 = N4,875,000`
* Utility of insured wealth:
  `U(w_insured) = ln(4,875,000) = 15.399620 utiles`

#### 3. Decision Rule:
* Compare `E[U(gamble)]` and `U(w_insured)`:
  * `E[U(gamble)] = 15.404538 utiles`
  * `U(w_insured) = 15.399620 utiles`
  * Difference: `15.404538 - 15.399620 = +0.004918 utiles`
* **Decision:**
  Since `E[U(gamble)] > U(w_insured)`, the individual attains greater expected satisfaction by bearing the risk than by purchasing insurance at the quoted fee of N125,000.  
  **The individual should NOT buy the insurance; he should take the gamble.**

---

### Method B: Certainty Equivalent Wealth (CEW) & Maximum Willingness to Pay

#### 1. Calculate Expected Wealth `E(w)`:
`E(w) = (0.50 * 6,000,000) + (0.50 * 4,000,000) = N5,000,000`  
*(Note: The gamble is actuarially neutral because expected net monetary gain is zero).*

#### 2. Calculate Certainty Equivalent Wealth (CEW):
`U(CEW) = E[U(w)] = 15.404538 utiles`  
`ln(CEW) = 15.404538`  
`CEW = exp(15.404538)`  

Alternatively, applying logarithmic laws directly:
`ln(CEW) = 0.5 * ln(6,000,000) + 0.5 * ln(4,000,000)`  
`ln(CEW) = ln( (6,000,000)^0.5 * (4,000,000)^0.5 )`  
`CEW = sqrt(6,000,000 * 4,000,000) = sqrt(24,000,000,000,000)`  
`CEW = N4,898,979.49`

#### 3. Calculate Maximum Risk Premium (`pi_max`):
The maximum fee the individual is willing to pay to eliminate the gamble equals their Risk Premium:
`Maximum Risk Premium = Expected Wealth - CEW`  
`pi_max = N5,000,000 - N4,898,979.49 = N101,020.51`

#### 4. Comparison with Quoted Insurance Fee:
* Maximum amount the individual is willing to pay for full insurance: **N101,020.51**
* Quoted insurance fee: **N125,000.00**
* The insurance company charges N125,000, which exceeds the individual's subjective risk premium of N101,020.51 by **N23,979.49**.
* **Final Exam Recommendation:**
  The individual should **reject the insurance offer and retain the gamble**, because the insurance premium (N125,000) exceeds their maximum willingness to pay (N101,020.51). Buying insurance would cause an economic welfare loss of N23,979.49 in certainty-equivalent wealth.
