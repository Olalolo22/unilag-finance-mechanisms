# FBA 414: Note 02 — Linear Programming: The Simplex Tableau Method
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 11)  
**Exam Focus:** Standard Form Conversion, Initial Tableau Setup, Pivot Row Operations, Optimality Criteria, Shadow Price Extraction.

---

## 1. The Core Intuition
When a Linear Programming problem has three or more decision variables, it cannot be solved on a two-dimensional graph. The **Simplex Algorithm** (developed by George Dantzig in 1947) is an algebraic procedure that systematically tests corner points (vertices) of the feasible solution space. 

Instead of evaluating all vertices blindly, the Simplex algorithm starts at the origin `(0, 0)`, checks if profit can be improved by introducing a non-zero variable, moves along the edge of the feasible polygon to an adjacent vertex with a higher profit, and terminates the moment no further improvement is mathematically possible.

---

## 2. The Step-by-Step Simplex Algorithm ("The Recipe")

### Step 1: Convert to Standard Equality Form
To perform matrix row operations, inequalities must be converted into strict equalities:
* For each `<=` constraint, add a **Slack Variable** (`s_i >= 0`). A slack variable represents unused or idle capacity.
  `a_1*x_1 + a_2*x_2 <= b_1`  ===>  `a_1*x_1 + a_2*x_2 + s_1 = b_1`
* Assign a coefficient of **0** to all slack variables in the objective function:
  `Maximize Z = c_1*x_1 + c_2*x_2 + 0*s_1 + 0*s_2`

### Step 2: Construct the Initial Simplex Tableau
1. **Basis Column:** Initially lists the slack variables (`s_1, s_2, ...`), representing the origin where real decision variables equal zero (`x_1 = 0, x_2 = 0`).
2. **`c_B` Column:** The profit coefficients of the basic variables in the objective function (initially all `0`).
3. **`c_j` Row (Top Header):** Lists the unit profit coefficients of all variables (`x_1, x_2, s_1, s_2`) from the objective function.
4. **Body Matrix:** The technological constraint coefficients `a_ij`.
5. **RHS (Solution) Column:** The available capacities `b_i`.
6. **`z_j` Row (Evaluation Row):**
   `z_j = SUM [ c_B * a_ij ]` (The opportunity cost of the resources consumed).
7. **`c_j - z_j` Row (Net Contribution / Indicator Row):**
   `Net Contribution = c_j - z_j` (The net profit gained by introducing one unit of variable `j` into the solution).

---

### Step 3: Test for Optimality
* **Maximization Rule:** If **all entries** in the `c_j - z_j` row are **zero or negative** (`<= 0`), the current tableau is **OPTIMAL**. Stop and read the solution.
* If any entry in `c_j - z_j` is strictly positive (`> 0`), the solution can be improved. Proceed to Step 4.

---

### Step 4: Determine Entering Variable (Key Column)
* Identify the column with the **largest positive value** in the `c_j - z_j` row.
* This is the **Key Column** (or Pivot Column). The corresponding variable will enter the basis.

---

### Step 5: Determine Leaving Variable (Key Row & Ratio Test)
* Divide each non-negative element of the RHS column by the strictly positive corresponding element in the Key Column:
  `Ratio = RHS_i / a_ik` (for `a_ik > 0`)
* **Rule:** Ignore zero or negative numbers in the denominator.
* Identify the row with the **smallest non-negative ratio**.
* This is the **Key Row** (or Pivot Row). The corresponding basic variable will leave the basis.

---

### Step 6: Identify Pivot Element & Execute Row Operations
* The number at the intersection of the Key Column and Key Row is the **Pivot Element** (or Key Element).
* **Row Operation 1 (New Pivot Row):**
  `New Pivot Row = Old Pivot Row / Pivot Element`
* **Row Operation 2 (All Other Rows):**
  `New Row = Old Row - (Key Column Coefficient of Old Row * New Pivot Row)`
* Recompute `z_j` and `c_j - z_j`. Return to Step 3.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Maximize `Z = 3*x_1 + 5*x_2`  
> Subject to:  
> `x_1 <= 4`  (Department 1)  
> `2*x_2 <= 12`  (Department 2)  
> `3*x_1 + 2*x_2 <= 18`  (Department 3)  
> `x_1 >= 0, x_2 >= 0`

---

### Step 1: Standard Equality Form
Introduce slack variables `s_1, s_2, s_3 >= 0`:
```text
Maximize Z = 3*x_1 + 5*x_2 + 0*s_1 + 0*s_2 + 0*s_3
Subject to:
1*x_1 + 0*x_2 + 1*s_1 + 0*s_2 + 0*s_3 = 4
0*x_1 + 2*x_2 + 0*s_1 + 1*s_2 + 0*s_3 = 12
3*x_1 + 2*x_2 + 0*s_1 + 0*s_2 + 1*s_3 = 18
```

---

### Step 2: Initial Simplex Tableau (Tableau 1)

```text
c_j  -->                 3      5      0      0      0
-----------------------------------------------------------------
c_B   Basis   RHS       x_1    x_2    s_1    s_2    s_3    Ratio
-----------------------------------------------------------------
 0     s_1     4         1      0      1      0      0     4 / 0 (Undefined)
 0     s_2    12         0     [2]     0      1      0    12 / 2 = 6  <-- (LEAVING ROW)
 0     s_3    18         3      2      0      0      1    18 / 2 = 9
-----------------------------------------------------------------
       z_j     0         0      0      0      0      0
   c_j - z_j   --        3     [5]     0      0      0
                                ^
                          (ENTERING COL)
```

#### Evaluation of Tableau 1:
1. **Key Column:** `x_2` has largest positive value in `c_j - z_j` (+5). So `x_2` enters.
2. **Key Row:** Ratios: Row 1 = N/A; Row 2 = `12 / 2 = 6`; Row 3 = `18 / 2 = 9`. Smallest ratio is 6 (Row 2, variable `s_2`). So `s_2` leaves.
3. **Pivot Element:** `2` (Row 2, Column `x_2`).

---

### Step 3: Second Simplex Tableau (Tableau 2)

#### Row Operations:
* `New Row 2 (Pivot Row) = Old Row 2 / 2`:
  `[ 12/2,  0/2,  2/2,  0/2,  1/2,  0/2 ]  ===>  [ 6,  0,  1,  0,  1/2,  0 ]`
* `New Row 1 = Old Row 1 - (0 * New Row 2)`:
  Row 1 has `0` in key column, so it remains unchanged: `[ 4,  1,  0,  1,  0,  0 ]`
* `New Row 3 = Old Row 3 - (2 * New Row 2)`:
  * RHS: `18 - 2*(6) = 6`
  * `x_1`: `3 - 2*(0) = 3`
  * `x_2`: `2 - 2*(1) = 0`
  * `s_1`: `0 - 2*(0) = 0`
  * `s_2`: `0 - 2*(1/2) = -1`
  * `s_3`: `1 - 2*(0) = 1`
  * `New Row 3 = [ 6,  3,  0,  0,  -1,  1 ]`

```text
c_j  -->                 3      5      0      0      0
-----------------------------------------------------------------
c_B   Basis   RHS       x_1    x_2    s_1    s_2    s_3    Ratio
-----------------------------------------------------------------
 0     s_1     4         1      0      1      0      0     4 / 1 = 4
 5     x_2     6         0      1      0     1/2     0     6 / 0 (Undefined)
 0     s_3     6        [3]     0      0     -1      1     6 / 3 = 2  <-- (LEAVING ROW)
-----------------------------------------------------------------
       z_j    30         0      5      0     5/2     0
   c_j - z_j   --       [3]     0      0    -5/2     0
                         ^
                   (ENTERING COL)
```

#### Evaluation of Tableau 2:
1. `c_j - z_j` has one positive entry (+3 under `x_1`). Solution is NOT optimal yet.
2. **Key Column:** `x_1` enters.
3. **Key Row:** Ratios: Row 1 = `4 / 1 = 4`; Row 3 = `6 / 3 = 2`. Smallest ratio is 2 (Row 3, variable `s_3`). So `s_3` leaves.
4. **Pivot Element:** `3` (Row 3, Column `x_1`).

---

### Step 4: Third Simplex Tableau (Tableau 3 — Final Optimal Tableau)

#### Row Operations:
* `New Row 3 (Pivot Row) = Old Row 3 / 3`:
  `[ 6/3,  3/3,  0/3,  0/3,  -1/3,  1/3 ]  ===>  [ 2,  1,  0,  0,  -1/3,  1/3 ]`
* `New Row 1 = Old Row 1 - (1 * New Row 3)`:
  * RHS: `4 - 1*(2) = 2`
  * `x_1`: `1 - 1*(1) = 0`
  * `x_2`: `0 - 1*(0) = 0`
  * `s_1`: `1 - 1*(0) = 1`
  * `s_2`: `0 - 1*(-1/3) = 1/3`
  * `s_3`: `0 - 1*(1/3) = -1/3`
  * `New Row 1 = [ 2,  0,  0,  1,  1/3,  -1/3 ]`
* `New Row 2 = Old Row 2 - (0 * New Row 3)`:
  Row 2 has `0` in key column, so it remains unchanged: `[ 6,  0,  1,  0,  1/2,  0 ]`

```text
c_j  -->                 3      5      0      0       0
-----------------------------------------------------------------
c_B   Basis   RHS       x_1    x_2    s_1    s_2     s_3
-----------------------------------------------------------------
 0     s_1     2         0      0      1     1/3    -1/3
 5     x_2     6         0      1      0     1/2      0
 3     x_1     2         1      0      0    -1/3     1/3
-----------------------------------------------------------------
       z_j    36         3      5      0     3/2      1
   c_j - z_j   --        0      0      0    -3/2     -1
```

#### Final Optimality Check:
All entries in the `c_j - z_j` row are **zero or negative** (`0, 0, 0, -1.5, -1`).  
Therefore, the **optimal solution is reached!**

---

### Step 5: Read the Final Solution & Shadow Prices

* **Optimal Production Schedule:**
  * `x_1 = 2` units
  * `x_2 = 6` units
  * Unused Slack: `s_1 = 2` hours idle in Department 1.
* **Maximum Profit `Z`:**
  `Z = 3*(2) + 5*(6) = 6 + 30 = N36` (matches RHS of `z_j` row!).
* **Shadow Prices (Dual Values):**
  Read directly from the `z_j` row under the slack columns:
  * Department 1 (`s_1`): `Shadow Price = 0` (Non-binding; 2 hours of idle time remain).
  * Department 2 (`s_2`): `Shadow Price = 1.5` (Binding; 1 extra hour yields N1.50 profit).
  * Department 3 (`s_3`): `Shadow Price = 1.0` (Binding; 1 extra hour yields N1.00 profit).

---

## 4. Exam Traps & Gotchas

1. **Tie in Key Column (Entering Variable):**
   * If two variables tie for largest positive in `c_j - z_j`, select arbitrarily (pick either). The algorithm will still reach optimality.
2. **Tie in Minimum Ratio (Leaving Variable):**
   * Indicates **Degeneracy**. Pick either row. In subsequent tableaus, one basic variable will take a value of zero.
3. **Negative / Zero Ratios:**
   * Never divide by zero or negative numbers in the ratio test! Denominator must be strictly positive (`> 0`).
4. **Minimization Problems:**
   * Two methods in UNILAG exams:
     * *Method A:* Convert to maximization by maximizing `-Z` (`Max -Z = -c_1*x_1 - c_2*x_2`).
     * *Method B:* In indicator row, select the **most negative** value to enter, and stop when all `c_j - z_j >= 0`.
