# FBA 414: Note 03 — The Assignment Problem: Hungarian Method & Variations
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 15)  
**Exam Focus:** Row/Column Reduction, Minimum Line Covering Test, Tableau Adjustment, Maximization Conversion, Prohibited Routes.

---

## 1. The Core Intuition
The **Assignment Problem** is a specialized linear programming model where $n$ facilities (workers, machines, trucks) must be assigned to $n$ tasks (jobs, locations, contracts) on a strict **one-to-one basis** (each worker gets exactly one task, and each task is performed by exactly one worker).

Because formulating this as a Simplex model requires $n \times n$ decision variables with integer constraints, Harold Kuhn developed the **Hungarian Method** (1955). The core mathematical insight is:  
> *If a constant is added to or subtracted from every element of any row or column of a cost matrix, the optimal assignment remains completely unchanged.*

The algorithm systematically reduces the cost matrix until an assignment can be made entirely using zero-cost cells.

---

## 2. The Step-by-Step Hungarian Algorithm ("The Recipe")

### Step 1: Check for Balance
* The matrix **must be square** (`Number of Rows = Number of Columns`).
* If `Rows > Columns`: Add a **Dummy Column** with zero costs (`0`) in every row.
* If `Columns > Rows`: Add a **Dummy Row** with zero costs (`0`) in every column.

### Step 2: Row Reduction
* Identify the **smallest element** in each row.
* Subtract this minimum value from every element in that row.
* *(Result: Every row now contains at least one zero).*

### Step 3: Column Reduction
* In the matrix resulting from Step 2, identify the **smallest element** in each column.
* Subtract this minimum value from every element in that column.
* *(Note: If a column already contains a zero from Step 2, its elements remain unchanged).*

### Step 4: Optimality Test (Minimum Line Covering)
* Draw the **minimum number of straight lines** (horizontal and/or vertical) required to cover **all zeros** in the reduced matrix.
* Let `L` = Number of lines drawn.
* Let `n` = Size of the matrix (number of rows/columns).
  * **If `L = n`:** The current matrix is **OPTIMAL**. Proceed immediately to Step 6 to make assignments.
  * **If `L < n`:** The matrix is **NOT optimal**. Proceed to Step 5 to generate more zeros.

### Step 5: Tableau Adjustment (Shifting Matrix Values)
1. Examine all numbers that are **NOT covered** by any line. Find the smallest uncovered value, call it `k`.
2. **Subtract `k`** from every **uncovered** element.
3. **Add `k`** to every element located at the **intersection of two lines**.
4. **Leave unchanged** all elements that are covered by only a **single line**.
5. Return to Step 4 and repeat the line covering test.

### Step 6: Make Unique Assignments
1. Scan the rows for a row with **exactly one zero**. Place a square `[0]` around it to assign that job, and draw an `X` through any other zeros in the same column.
2. Scan the columns for a column with **exactly one unassigned zero**. Box it `[0]`, and cross out any other zeros in that row.
3. Continue until every worker has exactly one assignment.
4. Calculate Total Cost by referencing the assigned cells back to the **original cost matrix**.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> A financial consulting firm has four project managers (A, B, C, D) and four corporate client audits (1, 2, 3, 4). The estimated audit completion costs (in thousands of Naira, N'000) are shown below:
>
> | Manager | Audit 1 | Audit 2 | Audit 3 | Audit 4 |
> | :---: | :---: | :---: | :---: | :---: |
> | **A** | 25 | 40 | 35 | 20 |
> | **B** | 30 | 60 | 40 | 35 |
> | **C** | 40 | 50 | 25 | 30 |
> | **D** | 45 | 40 | 30 | 25 |
>
> **Required:** Determine the optimal assignment of managers to audits that minimizes total completion cost, and compute the total cost.

---

### Step 1: Row Reduction
Find the minimum value in each row:
* Row A: min = `20` -> Subtract 20: `[ 5, 20, 15,  0 ]`
* Row B: min = `30` -> Subtract 30: `[ 0, 30, 10,  5 ]`
* Row C: min = `25` -> Subtract 25: `[ 15, 25,  0,  5 ]`
* Row D: min = `25` -> Subtract 25: `[ 20, 15,  5,  0 ]`

```text
Tableau after Row Reduction:
Manager     Audit 1   Audit 2   Audit 3   Audit 4
   A           5        20        15         0
   B           0        30        10         5
   C          15        25         0         5
   D          20        15         5         0
```

---

### Step 2: Column Reduction
Find the minimum value in each column:
* Col 1: min = `0` -> Unchanged: `[ 5,  0, 15, 20 ]`
* Col 2: min = `15` -> Subtract 15: `[ 5, 15, 10,  0 ]`
* Col 3: min = `0` -> Unchanged: `[ 15, 10,  0,  5 ]`
* Col 4: min = `0` -> Unchanged: `[ 0,  5,  5,  0 ]`

```text
Tableau after Column Reduction:
Manager     Audit 1   Audit 2   Audit 3   Audit 4
   A           5         5        15         0
   B           0        15        10         5
   C          15        10         0         5
   D          20         0         5         0
```

---

### Step 3: Optimality Test (Minimum Line Covering)
Cover all zeros with the minimum number of lines:
* **Line 1 (Vertical):** Column 4 covers zeros at (A, 4) and (D, 4).
* **Line 2 (Horizontal):** Row B covers zero at (B, 1).
* **Line 3 (Horizontal):** Row C covers zero at (C, 3).
* **Line 4 (Horizontal):** Row D covers zero at (D, 2) and (D, 4).

Wait! Can we cover all zeros in 3 lines?
* Column 4 covers (A, 4) and (D, 4).
* Column 1 covers (B, 1).
* Row C covers (C, 3).
* But (D, 2) is still uncovered!
* To cover (D, 2), we need a 4th line (either Row D or Column 2).

Minimum lines needed = **4 lines**.  
Since `L = 4 = n (size 4x4)`, the matrix is **OPTIMAL!**

---

### Step 4: Making the Final Assignments

```text
Optimality Matrix:
Manager     Audit 1   Audit 2   Audit 3   Audit 4
   A           5         5        15        [0]   <-- Only zero in Row A -> Assign (A, 4)
   B          [0]       15        10         5    <-- Only zero in Row B -> Assign (B, 1)
   C          15        10        [0]        5    <-- Only zero in Row C -> Assign (C, 3)
   D          20        [0]        5         X    <-- (D, 4) is crossed out; Assign (D, 2)
```

1. **Row A:** Has one zero at **Audit 4**. Assign **Manager A -> Audit 4**.  
   *(Cross out any other zero in Column 4, eliminating D4)*.
2. **Row B:** Has one zero at **Audit 1**. Assign **Manager B -> Audit 1**.
3. **Row C:** Has one zero at **Audit 3**. Assign **Manager C -> Audit 3**.
4. **Row D:** With D4 crossed out, only one zero remains at **Audit 2**. Assign **Manager D -> Audit 2**.

---

### Step 5: Total Cost Evaluation

| Manager | Assigned Audit | Original Cost (N'000) |
| :---: | :---: | :---: |
| **A** | Audit 4 | N20,000 |
| **B** | Audit 1 | N30,000 |
| **C** | Audit 3 | N25,000 |
| **D** | Audit 2 | N40,000 |
| **TOTAL** | | **N115,000** |

**Conclusion:** The optimal allocation yields a minimum total cost of **N115,000**.

---

## 4. Exam Traps & Variations (UNILAG Lecturer Tricks)

### Variation 1: Maximization Assignment (Profit / Revenue)
* **The Trap:** Students mistakenly run row reduction directly on profit numbers, which minimizes profit instead of maximizing it!
* **The Rule:** You **MUST** first convert the profit matrix into an **Opportunity Loss (Regret) Matrix**:
  1. Identify the **single largest number** in the entire matrix.
  2. Subtract **every element** in the matrix from this maximum number.
  3. Apply the standard Hungarian algorithm (Steps 1–6) to this new matrix.
  4. At the end, read final profit from the **original profit matrix**.

### Variation 2: Unbalanced Assignment Problems
* Example: 4 workers and 5 jobs (or 5 workers and 3 jobs).
* **The Rule:** Add a **dummy row** or **dummy column** filled with zeros.
* If a real worker is assigned to a dummy job in the solution, that worker is idle.

### Variation 3: Prohibited (Infeasible) Assignments
* Example: "Manager B cannot be assigned to Audit 2 due to a conflict of interest."
* **The Rule:** Replace the cost in cell `(B, 2)` with a very large penalty value: **`M`** (or `9999`).
* The algorithm will avoid assigning this cell at all costs.
