# FBA 414: Note 10 — Inventory Models: EOQ, Quantity Discounts & Reorder Levels
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 13); Dr. Adeleke, *FBA 410 Inventory Modeling*  
**Exam Focus:** Classical EOQ Derivation, Holding vs. Ordering Trade-Off, Quantity Discount Evaluation, Reorder Level (ROL), Minimum/Maximum Stock Control Levels.

---

## 1. The Core Intuition
Inventory represents tied-up working capital. The central managerial objective in inventory control is balancing two opposing financial forces:

1. **Ordering Costs (Setup Costs):** Costs incurred every time a purchase order is placed (clerical paperwork, delivery fees, inspection, shipping handling).  
   * *Behavior:* If you order in small batches frequently, annual ordering costs skyrocket.
2. **Holding Costs (Carrying Costs):** Costs of storing unsold inventory (warehouse rent, insurance, refrigeration, shrinkage, obsolescence, and the opportunity cost of capital).  
   * *Behavior:* If you order in massive batches to minimize ordering frequency, average inventory surges, and annual holding costs skyrocket.

The **Economic Order Quantity (EOQ)** is the exact mathematical batch size $Q^*$ where these two competing cost curves intersect, minimizing total annual inventory cost.

---

## 2. The Step-by-Step Mathematical Formulations ("The Recipe")

### Part A: The Classical EOQ Model (Wilson / Harris Model)

#### Assumptions:
1. Annual demand $D$ is constant and known with certainty.
2. Replenishment is instantaneous (entire order arrives in a single batch).
3. Lead time is zero or constant.
4. No shortages or stockouts are permitted.

#### Cost Equations:
* Let $D$ = Annual Demand (units per year).
* Let $C_o$ (or $S$) = Cost per order placed (Naira per order).
* Let $C_h$ (or $H$) = Holding cost per unit per year (Naira per unit per year).  
  *(Note: Often stated as a percentage $i$ of unit purchase price $C$: `C_h = i * C`).*
* Let $Q$ = Order quantity (batch size).

1. **Annual Ordering Cost:**
   `Number of Orders per Year = D / Q`
   `Annual Ordering Cost = (D / Q) * C_o`

2. **Annual Holding Cost:**
   `Average Inventory Level = Q / 2`
   `Annual Holding Cost = (Q / 2) * C_h`

3. **Total Annual Inventory Cost (`TC`):**
   `Total Cost = Annual Purchase Cost + Annual Ordering Cost + Annual Holding Cost`
   `TC = (D * C) + [ (D / Q) * C_o ] + [ (Q / 2) * C_h ]`

#### Derivation of EOQ ($Q^*$):
Take the first derivative of $TC$ with respect to $Q$ and set it to zero:
`d(TC) / dQ = -(D * C_o) / Q^2 + C_h / 2 = 0`  
`(D * C_o) / Q^2 = C_h / 2`  
`Q^2 = (2 * D * C_o) / C_h`  
`EOQ = Q* = sqrt( (2 * D * C_o) / C_h )`

#### Golden Rule of Classical EOQ:
At the optimal order quantity $Q^*$, **Annual Ordering Cost equals Annual Holding Cost exactly**:
`(D / Q*) * C_o = (Q* / 2) * C_h`

---

### Part B: EOQ with Quantity Discounts (Price Breaks)

Suppliers frequently offer price discounts if a firm purchases large lot sizes (e.g., N100/unit for orders under 1,000 units, but N95/unit for orders of 1,000 units or more).

#### Evaluation Procedure:
1. **Step 1:** Calculate EOQ at the **lowest unit price** (highest discount tier).
2. **Step 2:** Check if that calculated EOQ is **feasible** (i.e., falls within the quantity range required to qualify for that discount).
   * If feasible: Compute Total Annual Cost (`TC = D*C + (D/Q)*C_o + (Q/2)*C_h`). This is the global optimum!
   * If not feasible (EOQ is below the qualifying minimum): Compute Total Annual Cost at the **minimum qualifying threshold point** for that discount.
3. **Step 3:** Calculate EOQ and Total Cost at the next lower discount tier.
4. **Step 4:** Compare the total annual costs across all evaluated options. Select the order quantity that minimizes **Total Cost** (which MUST include total purchase price `D * C`).

---

### Part C: Stock Control Levels & Safety Stock

Under lead time uncertainty, inventory managers set threshold stock levels:

1. **Reorder Level (ROL):** The stock level that automatically triggers a new order:
   `ROL = Maximum Usage Rate * Maximum Lead Time`
2. **Minimum Stock Level (Safety / Buffer Stock):** The lower safety margin preventing stockouts:
   `Minimum Level = ROL - (Normal / Average Usage Rate * Normal / Average Lead Time)`
3. **Maximum Stock Level:** Prevents excessive capital lockup and storage congestion:
   `Maximum Level = ROL + EOQ - (Minimum Usage Rate * Minimum Lead Time)`
4. **Average Stock Level:**
   `Average Stock = Minimum Stock Level + (EOQ / 2)`

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Golden Flour Mills Ltd uses wheat grain at a steady rate of **10,000 bags per year**.  
> The relevant cost data is as follows:
> * Purchase price: **N2,000 per bag**.
> * Ordering cost: **N500 per order** placed.
> * Annual inventory holding cost: **10% of the unit purchase price**.
> * Working year: **250 days**. Lead time: **5 working days**.
>
> A bulk grain supplier offers a **2% discount** on purchase price if Golden Flour Mills orders in batches of at least **1,000 bags**.
>
> **Required:**  
> (a) Compute the standard Economic Order Quantity (EOQ), optimal number of orders per year, and the Reorder Level.  
> (b) Calculate the total annual inventory cost under the standard EOQ.  
> (c) Advise management on whether to accept the supplier’s quantity discount offer of 2% for orders of 1,000 bags.

---

### Step 1: Classical EOQ & Reorder Level Calculations

* `Annual Demand (D) = 10,000 bags`
* `Unit Price (C) = N2,000`
* `Ordering Cost (C_o) = N500`
* `Holding Cost (C_h) = 10% of N2,000 = 0.10 * 2,000 = N200 per bag/year`

#### 1. Economic Order Quantity (`EOQ`):
`EOQ = sqrt( (2 * D * C_o) / C_h )`  
`EOQ = sqrt( (2 * 10,000 * 500) / 200 )`  
`EOQ = sqrt( 10,000,000 / 200 ) = sqrt( 50,000 ) = 223.6 bags` (approx. **224 bags**).

#### 2. Number of Orders per Year (`N*`):
`N* = D / EOQ = 10,000 / 223.6 = 44.7 orders per year`

#### 3. Cycle Time (Time Between Orders):
`Cycle Time = 250 working days / 44.7 = 5.59 working days`

#### 4. Reorder Level (`ROL`):
`Daily Demand = 10,000 / 250 = 40 bags per day`  
`Lead Time = 5 days`  
`ROL = Daily Demand * Lead Time = 40 * 5 = 200 bags`  
*(Place a new order the moment inventory drops to 200 bags).*

---

### Step 2: Total Cost Under Standard EOQ ($Q = 224$)

1. **Purchase Cost:** `D * C = 10,000 * 2,000 = N20,000,000`
2. **Annual Ordering Cost:** `(10,000 / 223.6) * 500 = N22,360.68`
3. **Annual Holding Cost:** `(223.6 / 2) * 200 = N22,360.00`
   *(Notice how ordering and holding costs are equal at EOQ!)*
4. **Total Annual Cost:**
   `TC_standard = 20,000,000 + 22,360.68 + 22,360.00 = N20,044,720.68`

---

### Step 3: Evaluate Quantity Discount ($Q = 1,000$ bags)

* Discounted Unit Price: `C_disc = 2,000 * (1 - 0.02) = N1,960 per bag`
* Discounted Holding Cost: `C_h_disc = 10% of N1,960 = N196 per bag/year`
* Order Quantity: `Q = 1,000 bags`

1. **Purchase Cost:** `10,000 * 1,960 = N19,600,000`  
   *(Generates a direct purchase price savings of `N400,000`!)*
2. **Annual Ordering Cost:** `(10,000 / 1,000) * 500 = 10 orders * 500 = N5,000`
3. **Annual Holding Cost:** `(1,000 / 2) * 196 = 500 * 196 = N98,000`
4. **Total Annual Cost under Discount:**
   `TC_discount = 19,600,000 + 5,000 + 98,000 = N19,703,000.00`

---

### Step 4: Comparison & Final Recommendation

| Cost Component | Standard EOQ ($Q = 224$) | Discount Offer ($Q = 1,000$) | Difference (Savings) |
| :--- | :--- | :--- | :--- |
| **Annual Purchase Cost** | N20,000,000.00 | N19,600,000.00 | **+N400,000.00** (Saved) |
| **Annual Ordering Cost** | N22,360.68 | N5,000.00 | **+N17,360.68** (Saved) |
| **Annual Holding Cost** | N22,360.00 | N98,000.00 | **-N75,640.00** (Extra Cost) |
| **TOTAL ANNUAL COST** | **N20,044,720.68** | **N19,703,000.00** | **+N341,720.68 Net Savings** |

**Managerial Recommendation:**  
Golden Flour Mills **should accept the 2% quantity discount offer** and order in batches of 1,000 bags.  
Although holding costs increase by N75,640 due to higher average stock levels, this is vastly outweighed by N400,000 in purchase cost savings and N17,361 in order processing savings, delivering a **net annual financial gain of N341,720.68**.

---

## 4. Exam Traps & Gotchas

1. **Ignoring Purchase Cost in Discount Problems:**
   * In a standard EOQ problem with a fixed price, purchase cost `D * C` is omitted because it is constant.
   * **In quantity discount problems, you MUST include `D * C`**, because the bulk price reduction (`N400,000`) is typically the dominant financial factor!
2. **Recomputing Holding Cost (`C_h`):**
   * If holding cost is given as a percentage of purchase price (e.g., 10%), remember to multiply by the **new discounted price** (`0.10 * 1,960 = 196`), not the original price!
3. **Rounding EOQ:**
   * EOQ represents a physical batch quantity. When reporting final recommendations, round to the nearest whole unit (e.g., 223.6 -> 224 bags).

