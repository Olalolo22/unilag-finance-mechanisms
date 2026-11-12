# FBA 414: Note 05 — The Transportation Problem: NW Corner, VAM & MODI Method
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 14)  
**Exam Focus:** Balance Verification, North-West Corner Rule, Vogel’s Approximation Method (VAM), Degeneracy Test (`m + n - 1`), MODI (u-v) Optimality Test.

---

## 1. The Core Intuition
The **Transportation Problem** is a specialized linear programming model designed to find the most cost-effective shipping schedule for distributing a homogeneous commodity from $m$ origins (factories/warehouses with known capacities) to $n$ destinations (markets/distribution centers with known demands).

Because each unit shipped from origin $i$ to destination $j$ incurs a fixed unit transportation cost $c_{ij}$, the objective is to minimize total freight cost while strictly satisfying both factory supply limits and destination demand requirements.

---

## 2. The Step-by-Step Algorithm ("The Recipe")

### Step 1: Verify Balance
* Sum total supply: `Total Supply = SUM(Supply_i)`
* Sum total demand: `Total Demand = SUM(Demand_j)`
* **If `Supply = Demand`:** The problem is **Balanced**.
* **If `Supply > Demand`:** Add a **Dummy Destination** with demand equal to `(Supply - Demand)` and unit shipping costs of **`0`**.
* **If `Demand > Supply`:** Add a **Dummy Origin** with capacity equal to `(Demand - Supply)` and unit shipping costs of **`0`**.

---

### Step 2: Generate Initial Basic Feasible Solution (IBFS)
Two primary methods are tested in UNILAG exams:

#### Method A: North-West Corner Rule (Simple, but ignores costs)
1. Start at the top-leftmost cell `(Row 1, Column 1)`.
2. Allocate the maximum possible units: `Quantity = min(Supply_1, Demand_1)`.
3. Subtract the allocated quantity from both row supply and column demand:
   * If row supply becomes `0`, move **down** to `(Row 2, Column 1)`.
   * If column demand becomes `0`, move **right** to `(Row 1, Column 2)`.
4. Repeat until all supply and demand are fully exhausted.

#### Method B: Vogel's Approximation Method — VAM (Heuristic, near-optimal)
1. **Calculate Penalties:** For every row and column, identify the **two lowest costs**. Compute the penalty = `(Second Lowest Cost - Lowest Cost)`.
2. **Select Key Line:** Identify the row or column with the **largest penalty**. (If a tie occurs, break it by selecting the line containing the absolute lowest cost cell).
3. **Allocate:** In that selected row/column, locate the cell with the **lowest unit cost**. Allocate the maximum possible amount: `min(Supply, Demand)`.
4. **Cross Out:** Cross out the exhausted row or column.
5. Recompute penalties for the remaining rows and columns. Repeat until all allocations are complete.

---

### Step 3: Degeneracy Test (MANDATORY EXAM CHECK)
* Count the total number of occupied (allocated) cells.
* **Non-Degeneracy Condition:**
  `Number of Occupied Cells = m + n - 1`
  *(where `m` = number of rows, `n` = number of columns).*
* **If `Occupied Cells < m + n - 1`:** The solution is **Degenerate**.
  * **Fix:** Allocate an infinitesimally small quantity **`epsilon`** (or `e`) to an unallocated cell that does not form a closed loop (usually the unoccupied cell with the lowest unit cost).

---

### Step 4: Optimality Test using Modified Distribution (MODI / u-v Method)
1. For every **occupied (allocated) cell**, the transportation cost must satisfy:
   `u_i + v_j = c_ij`
   * Where `u_i` is the row dual value and `v_j` is the column dual value.
2. Set `u_1 = 0` as an arbitrary starting reference, and solve for all `u_i` and `v_j` values across occupied cells.
3. For every **unoccupied (empty) cell**, compute the **Opportunity Cost / Net Evaluation (`d_ij`)**:
   `d_ij = c_ij - (u_i + v_j)`
4. **Optimality Criteria:**
   * **If all `d_ij >= 0`:** The solution is **OPTIMAL**! Calculate total cost.
   * **If any `d_ij < 0`:** The solution is **NOT optimal**. Cost can be further reduced. Proceed to Step 5.

---

### Step 5: Stepping-Stone Closed Loop Revision (If not optimal)
1. Select the unoccupied cell with the **most negative `d_ij`** as the **Entering Cell**.
2. Trace a **Closed Loop** starting and ending at the entering cell:
   * The loop consists only of horizontal and vertical line segments.
   * Every turn (corner) of the loop **must be on an occupied cell**.
3. Place alternating signs around the corners: `+` at the entering cell, `-` at the first turn, `+` at the second turn, `-` at the third turn.
4. Find the smallest quantity among all cells with a **`-` sign**, call it `theta`.
5. Shift allocations:
   * Add `theta` to all cells with `+` signs.
   * Subtract `theta` from all cells with `-` signs.
6. Re-test with MODI until all `d_ij >= 0`.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Dangote Cement operates three manufacturing plants (P1, P2, P3) supplying cement to three regional depots (D1, D2, D3). The unit transportation costs (N'000 per ton), factory capacities, and depot demands are:
>
> ```text
>               D1       D2       D3      Supply (Tons)
>       P1    [  4        8        8   ]       76
>       P2    [ 16       24       16   ]       82
>       P3    [  8       16       24   ]       77
> Demand (Tons) 72       102       61        Total = 235
> ```
>
> **Required:**  
> (a) Find the Initial Basic Feasible Solution using Vogel's Approximation Method (VAM).  
> (b) Test for optimality using the MODI method and calculate the minimum total freight cost.

---

### Step 1: Vogel's Approximation Method (VAM) Iterations

#### Initial Penalty Calculations:
* Row P1 costs: `[ 4, 8, 8 ]` -> Two lowest: `4, 8` -> Penalty = `8 - 4 = 4`
* Row P2 costs: `[ 16, 24, 16 ]` -> Two lowest: `16, 16` -> Penalty = `16 - 16 = 0`
* Row P3 costs: `[ 8, 16, 24 ]` -> Two lowest: `8, 16` -> Penalty = `16 - 8 = 8`
* Col D1 costs: `[ 4, 16, 8 ]` -> Two lowest: `4, 8` -> Penalty = `8 - 4 = 4`
* Col D2 costs: `[ 8, 24, 16 ]` -> Two lowest: `8, 16` -> Penalty = `16 - 8 = 8`
* Col D3 costs: `[ 8, 16, 24 ]` -> Two lowest: `8, 16` -> Penalty = `16 - 8 = 8`

**Highest Penalty:** A three-way tie at `8` (Row P3, Col D2, Col D3).  
Look for the lowest cost cell among them: Row P1 has cost `8` in D2/D3; Row P3 has cost `8` in D1; Col D2 has cost `8` in P1.  
Select **Row P3** (lowest cost is cell `(P3, D1)` with cost `8`):
* Allocate to `(P3, D1)`: `min(Supply P3 = 77, Demand D1 = 72) = 72 tons`.
* Depot D1 demand is satisfied (remaining = 0). Cross out Column D1.
* Row P3 remaining supply = `77 - 72 = 5 tons`.

#### Next Iteration (Columns D2 and D3 remaining):
* Row P1 remaining: `[ 8, 8 ]` -> Penalty = `8 - 8 = 0`
* Row P2 remaining: `[ 24, 16 ]` -> Penalty = `24 - 16 = 8`
* Row P3 remaining: `[ 16, 24 ]` -> Penalty = `24 - 16 = 8`
* Col D2 remaining: `[ 8, 24, 16 ]` -> Lowest: `8, 16` -> Penalty = `16 - 8 = 8`
* Col D3 remaining: `[ 8, 16, 24 ]` -> Lowest: `8, 16` -> Penalty = `16 - 8 = 8`

Select **Col D2** (lowest cost cell is `(P1, D2)` with cost `8`):
* Allocate to `(P1, D2)`: `min(Supply P1 = 76, Demand D2 = 102) = 76 tons`.
* Plant P1 capacity is fully exhausted. Cross out Row P1.
* Depot D2 remaining demand = `102 - 76 = 26 tons`.

#### Next Iteration (Rows P2 and P3, Columns D2 and D3 remaining):
* Allocate remaining P3 supply (5 tons) to lowest cost cell `(P3, D2)` at cost `16`:
  * Allocate 5 tons to `(P3, D2)`. Row P3 exhausted.
  * Depot D2 remaining demand = `26 - 5 = 21 tons`.
* Now only Plant P2 remains (capacity = 82 tons):
  * Allocate 21 tons to `(P2, D2)` at cost `24` -> D2 demand fully satisfied!
  * Allocate remaining 61 tons to `(P2, D3)` at cost `16` -> D3 demand fully satisfied!

---

### Step 2: Summary of VAM Initial Allocations

```text
              D1             D2             D3        Supply
      P1     --            [ 76 ]         --            76
                         (cost: 8)
      P2     --            [ 21 ]         [ 61 ]        82
                         (cost: 24)     (cost: 16)
      P3   [ 72 ]          [  5 ]         --            77
          (cost: 8)      (cost: 16)
------------------------------------------------------------
Demand       72             102             61         235
```

---

### Step 3: Degeneracy Check
* `m = 3` rows, `n = 3` columns.
* Required occupied cells = `m + n - 1 = 3 + 3 - 1 = 5 cells`.
* Actual occupied cells = `5 cells` (P1-D2, P2-D2, P2-D3, P3-D1, P3-D2).
* **Condition satisfied:** The solution is non-degenerate.

---

### Step 4: MODI (u-v) Optimality Test

Set up `u_i + v_j = c_ij` for all 5 occupied cells:
1. Set **`u_1 = 0`**.
2. For Cell `(P1, D2)`: `u_1 + v_2 = 8`  ===> `0 + v_2 = 8`  ===> **`v_2 = 8`**.
3. For Cell `(P2, D2)`: `u_2 + v_2 = 24` ===> `u_2 + 8 = 24` ===> **`u_2 = 16`**.
4. For Cell `(P2, D3)`: `u_2 + v_3 = 16` ===> `16 + v_3 = 16` ===> **`v_3 = 0`**.
5. For Cell `(P3, D2)`: `u_3 + v_2 = 16` ===> `u_3 + 8 = 16` ===> **`u_3 = 8`**.
6. For Cell `(P3, D1)`: `u_3 + v_1 = 8`  ===> `8 + v_1 = 8`  ===> **`v_1 = 0`**.

#### Evaluate Unoccupied Cells (`d_ij = c_ij - u_i - v_j`):
* **Cell (P1, D1):** `d_11 = 4 - (u_1 + v_1) = 4 - (0 + 0) = +4 >= 0`
* **Cell (P1, D3):** `d_13 = 8 - (u_1 + v_3) = 8 - (0 + 0) = +8 >= 0`
* **Cell (P2, D1):** `d_21 = 16 - (u_2 + v_1) = 16 - (16 + 0) = 0 >= 0`
* **Cell (P3, D3):** `d_33 = 24 - (u_3 + v_3) = 24 - (8 + 0) = +16 >= 0`

**Optimality Conclusion:**
All net evaluations `d_ij >= 0` (`+4, +8, 0, +16`).  
**The VAM initial solution is already 100% OPTIMAL!**

---

### Step 5: Total Minimum Transportation Cost Calculation

| Route | Tons Shipped | Unit Cost (N'000) | Total Cost (N'000) |
| :---: | :---: | :---: | :---: |
| **P1 -> D2** | 76 | N8 | N608 |
| **P2 -> D2** | 21 | N24 | N504 |
| **P2 -> D3** | 61 | N16 | N976 |
| **P3 -> D1** | 72 | N8 | N576 |
| **P3 -> D2** | 5 | N16 | N80 |
| **TOTAL** | **235 tons** | | **N2,744 (N2,744,000)** |

---

## 4. Exam Traps & Gotchas

1. **Unbalanced Matrices:** Never start allocating before summing rows and columns! If supply does not equal demand, add a dummy line with `0` costs.
2. **Degeneracy Trap (`Occupied < m + n - 1`):**
   * If a single allocation simultaneously exhausts both a row and a column, the next step will result in fewer than `m + n - 1` occupied cells.
   * If you try to calculate `u_i` and `v_j`, you will find an insolvable variable. You **MUST** insert an `epsilon` (`e`) to restore connectivity.
3. **Loop Construction Rules:**
   * A stepping stone loop must alternate horizontal and vertical steps.
   * Every turn must land on an occupied cell. You can jump over unoccupied or occupied cells without turning on them.
