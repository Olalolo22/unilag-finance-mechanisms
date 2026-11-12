# FBA 414: Note 01 — Linear Programming: Formulation & The Graphical Method
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapters 10–11)  
**Exam Focus:** Problem Formulation, Boundary Intercept Calculations, Feasible Region Identification, Corner Point Evaluation.

---

## 1. The Core Intuition
Linear Programming (LP) is a deterministic optimization technique used by management to allocate scarce organizational resources (such as machine hours, labor, raw materials, or capital) among competing activities to achieve an optimal objective—either maximizing total profit or minimizing total production cost.

Every LP problem assumes:
1. **Proportionality:** The contribution of each variable to the objective and constraints is directly proportional to its value.
2. **Additivity:** Total contribution equals the sum of individual contributions.
3. **Divisibility:** Decision variables can take fractional (continuous) values.
4. **Certainty:** All coefficients are known and constant.

---

## 2. The Step-by-Step Formulation & Graphical Algorithm

### Part A: Mathematical Formulation ("The Recipe")
* **Step 1 (Define Decision Variables):** Explicitly define the unknown quantities the manager must choose.
  * Let `x_1` = Number of units of Product 1 to produce per period.
  * Let `x_2` = Number of units of Product 2 to produce per period.
* **Step 2 (State the Objective Function):** Express total profit or cost as a linear equation.
  * Maximization: `Maximize Z = c_1 * x_1 + c_2 * x_2`
  * Minimization: `Minimize Z = c_1 * x_1 + c_2 * x_2`
  * Where `c_1, c_2` are unit contributions/costs.
* **Step 3 (Formulate Structural Constraints):** Express resource limitations or minimum requirements as linear inequalities (`<=` for capacity limits; `>=` for minimum quotas).
  * `a_11 * x_1 + a_12 * x_2 <= b_1` (Resource 1 capacity)
  * `a_21 * x_1 + a_22 * x_2 <= b_2` (Resource 2 capacity)
* **Step 4 (Specify Non-Negativity Constraints):** Variables cannot be negative.
  * `x_1 >= 0, x_2 >= 0`

---

### Part B: The Graphical Solution Method (for 2-Variable Problems)
* **Step 1 (Find Boundary Intercepts):** Convert each inequality constraint into an equality equation. Find the two axis intercept points for each constraint line:
  * Set `x_1 = 0` and solve for `x_2`. Intercept is `(0, x_2)`.
  * Set `x_2 = 0` and solve for `x_1`. Intercept is `(x_1, 0)`.
* **Step 2 (Plot and Determine Half-Spaces):**
  * Draw the axes (`x_1` on horizontal axis, `x_2` on vertical axis).
  * Connect the intercept points for each constraint.
  * Test point `(0, 0)`:
    * If `(0, 0)` satisfies the inequality (e.g. `0 <= b`), shade toward the origin.
    * If `(0, 0)` violates the inequality (e.g. `0 >= b`), shade away from the origin.
* **Step 3 (Identify the Feasible Region):** The feasible region is the polygon that satisfies **all** constraints simultaneously, bounded by the axes in the non-negative quadrant.
* **Step 4 (Corner Point Method):**
  * By the Fundamental Theorem of Linear Programming, if an optimal solution exists, it **must** occur at one of the corner points (vertices) of the feasible region.
  * Identify all vertices: `A, B, C, D, ...`
  * For intersection vertices, solve the two intersecting boundary equations simultaneously.
* **Step 5 (Evaluate Z and Select the Optimum):**
  * Substitute the `(x_1, x_2)` coordinates of every corner point into the objective function `Z`.
  * For Maximization: Select the vertex yielding the highest `Z`.
  * For Minimization: Select the vertex yielding the lowest `Z`.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Apex Manufacturing Ltd produces two types of executive chairs: **Standard (x_1)** and **Deluxe (x_2)**.  
> Production requires processing in two distinct departments: **Fabrication** and **Finishing**.  
> * Each Standard chair requires 4 hours of Fabrication and 2 hours of Finishing.  
> * Each Deluxe chair requires 3 hours of Fabrication and 3 hours of Finishing.  
> * Total available hours per week: Fabrication = 48 hours; Finishing = 30 hours.  
> * Unit profit contribution: Standard chair = N40; Deluxe chair = N30.  
> 
> **Required:**  
> (a) Formulate the Linear Programming model.  
> (b) Solve graphically to find the profit-maximizing weekly production schedule and maximum profit.

---

### Solution Walkthrough:

#### (a) Model Formulation
* **Decision Variables:**
  * Let `x_1` = Number of Standard chairs to produce per week.
  * Let `x_2` = Number of Deluxe chairs to produce per week.
* **Objective Function:**
  `Maximize Z = 40*x_1 + 30*x_2`
* **Subject to Constraints:**
  * Fabrication capacity: `4*x_1 + 3*x_2 <= 48`
  * Finishing capacity: `2*x_1 + 3*x_2 <= 30`
  * Non-negativity: `x_1 >= 0, x_2 >= 0`

---

#### (b) Graphical Solution

##### Step 1: Calculate Boundary Intercepts
* **Constraint 1 (Fabrication): `4*x_1 + 3*x_2 = 48`**
  * When `x_1 = 0`: `3*x_2 = 48` => `x_2 = 16`. Point: `(0, 16)`
  * When `x_2 = 0`: `4*x_1 = 48` => `x_1 = 12`. Point: `(12, 0)`
* **Constraint 2 (Finishing): `2*x_1 + 3*x_2 = 30`**
  * When `x_1 = 0`: `3*x_2 = 30` => `x_2 = 10`. Point: `(0, 10)`
  * When `x_2 = 0`: `2*x_1 = 30` => `x_1 = 15`. Point: `(15, 0)`

---

##### Step 2: Define Feasible Region Vertices
The feasible region is bounded by the non-negativity axes and the tighter constraints:
* **Point O (Origin):** `(0, 0)`
* **Point A (Finishing y-intercept):** `(0, 10)`
* **Point C (Fabrication x-intercept):** `(12, 0)`  
  *(Note: `(15, 0)` is infeasible because `4*(15) + 3*(0) = 60 > 48`).*
* **Point B (Intersection of Fabrication and Finishing):**
  Solve the two simultaneous equations:
  ```text
  Equation 1:  4*x_1 + 3*x_2 = 48
  Equation 2:  2*x_1 + 3*x_2 = 30
  ```
  Subtract Equation 2 from Equation 1:
  ```text
  (4*x_1 - 2*x_1) + (3*x_2 - 3*x_2) = 48 - 30
  2*x_1 = 18
  x_1 = 9
  ```
  Substitute `x_1 = 9` into Equation 2:
  ```text
  2*(9) + 3*x_2 = 30
  18 + 3*x_2 = 30
  3*x_2 = 12
  x_2 = 4
  ```
  Therefore, Point B has coordinates: `(9, 4)`.

---

##### Step 3: Corner Point Evaluation Table

| Corner Point | Coordinates `(x_1, x_2)` | Profit Function `Z = 40*x_1 + 30*x_2` | Total Profit (Naira) |
| :--- | :--- | :--- | :--- |
| **Point O** | `(0, 0)` | `40*(0) + 30*(0)` | **N0** |
| **Point A** | `(0, 10)` | `40*(0) + 30*(10)` | **N300** |
| **Point B** | `(9, 4)` | `40*(9) + 30*(4) = 360 + 120` | **N480 (OPTIMAL)** |
| **Point C** | `(12, 0)` | `40*(12) + 30*(0)` | **N480 (OPTIMAL)** |

*Wait! Look closely at Point B and Point C:*
* `Z(Point B) = 40*(9) + 30*(4) = 360 + 120 = N480`
* `Z(Point C) = 40*(12) + 30*(0) = 480 + 0 = N480`

Both Point B and Point C yield the exact same maximum profit of **N480**!

---

## 4. Exam Traps & Special Cases

### Trap 1: Multiple (Alternate) Optimal Solutions
* Notice in the problem above, the slope of the objective function is:
  `Slope of Z = -(c_1 / c_2) = -(40 / 30) = -4/3`
* The slope of the Fabrication constraint boundary line is:
  `Slope of Fabrication = -(a_11 / a_12) = -(4 / 3) = -4/3`
* **Exam Rule:** Whenever the slope of the objective function equals the slope of a binding constraint, **multiple optimal solutions exist**.
* Any linear combination of points along the line segment connecting Point B `(9, 4)` and Point C `(12, 0)` is optimal and yields `Z = N480`.

### Trap 2: Infeasibility
* Occurs when no single point satisfies all constraints simultaneously (e.g., `x_1 + x_2 <= 5` and `x_1 + x_2 >= 10`).
* In the exam, state: *"The feasible region is null; no solution exists."*

### Trap 3: Unboundedness
* Occurs in maximization problems when the feasible region is open (unconstrained in the positive direction), allowing `Z` to increase infinitely without violating constraints.
* In the exam, state: *"The solution space is unbounded; profit can grow to infinity."*

### Trap 4: Redundant Constraints
* A constraint that does not touch or restrict the feasible region. Removing it changes nothing. Do not waste time computing its intersections!

