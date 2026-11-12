# FBA 414: Note 06 — Project Management: CPM, PERT & Project Crashing
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapters 17–18)  
**Exam Focus:** Network Construction, Forward/Backward Pass (ES, EF, LS, LF), Float Calculations (Total, Free, Independent), PERT Expected Time & Variance, Project Crashing Cost Slopes.

---

## 1. The Core Intuition
Project Management through **Network Analysis** enables managers to schedule, monitor, and control complex projects composed of dozens or hundreds of individual, interdependent activities.

* **Critical Path Method (CPM):** Used for deterministic projects where activity durations are known with certainty (e.g., standard construction or factory overhaul). Identifies the longest continuous sequence of dependent tasks—the **Critical Path**—which dictates the minimum completion time of the entire project.
* **Program Evaluation and Review Technique (PERT):** Used for probabilistic, research-and-development projects where activity durations are uncertain. Uses three time estimates (Optimistic, Most Likely, Pessimistic) modeled on a Beta distribution to calculate completion probabilities.

---

## 2. The Step-by-Step CPM & PERT Algorithms ("The Recipe")

### Part A: CPM Forward & Backward Pass (Deterministic)

#### 1. Forward Pass (Earliest Times):
* Start at the first event (Event 1): Set `Earliest Start (ES) = 0`.
* Move left-to-right through the network:
  `Earliest Finish (EF) = Earliest Start (ES) + Duration (D)`
* **Merge Rule:** When multiple activities enter a node, the Earliest Start of the succeeding activity equals the **MAXIMUM** of the Earliest Finishes of its immediate predecessors:
  `ES_j = MAX [ EF of all predecessors ]`

#### 2. Backward Pass (Latest Times):
* Start at the final completion event: Set `Latest Finish (LF) = Earliest Finish (EF)`.
* Move right-to-left through the network:
  `Latest Start (LS) = Latest Finish (LF) - Duration (D)`
* **Burst Rule:** When multiple activities leave a node, the Latest Finish of the preceding activity equals the **MINIMUM** of the Latest Starts of its immediate successors:
  `LF_i = MIN [ LS of all successors ]`

#### 3. Float (Slack) Calculations:
* **Total Float (TF):** The amount of time an activity can be delayed without delaying the overall project completion date:
  `Total Float = LF - EF = LS - ES`
* **Free Float (FF):** The amount of time an activity can be delayed without delaying the early start of any immediate successor:
  `Free Float = ES_(successor) - EF`
* **Independent Float (IF):** Float that arises regardless of predecessor/successor timing:
  `Independent Float = max(0, ES_(successor) - LF_(predecessor) - D)`

#### 4. Identify the Critical Path:
* An activity is **Critical** if and only if:
  1. `ES = LS` (Earliest Start equals Latest Start).
  2. `EF = LF` (Earliest Finish equals Latest Finish).
  3. `Total Float = 0`.
* The **Critical Path** connects all critical activities from start to finish. Any delay on this path directly delays the entire project!

---

### Part B: PERT Probabilistic Durations
When activity times are uncertain, three time estimates are provided:
* `a` = **Optimistic Time:** Best-case duration assuming everything goes perfectly.
* `m` = **Most Likely Time:** Normal duration under standard operating conditions (the mode).
* `b` = **Pessimistic Time:** Worst-case duration assuming severe delays.

#### Formulas:
1. **Expected Duration (`t_e`):**
   `t_e = (a + 4*m + b) / 6`
2. **Variance of Activity (`sigma^2`):**
   `sigma^2 = [ (b - a) / 6 ]^2`
3. **Project Expected Completion Time (`T_e`):**
   `T_e = SUM [ t_e of activities on Critical Path ]`
4. **Project Standard Deviation (`sigma_proj`):**
   `sigma_proj = sqrt( SUM [ sigma^2 of activities on Critical Path ] )`
   *(Rule: Sum variances of critical activities ONLY, then take square root).*
5. **Probability of Finishing by Due Date (`D`):**
   Compute Z-Score:
   `Z = (Due Date - T_e) / sigma_proj`
   Look up `Z` on the standard normal distribution table.

---

### Part C: Project Crashing (Time-Cost Optimization)
To shorten a project deadline at minimum incremental expense:
1. Compute the **Crash Cost Slope** for every activity:
   `Cost Slope = (Crash Cost - Normal Cost) / (Normal Time - Crash Time)`
   *(Represents the additional cost per week/day to expedite the task).*
2. **Crash Rule:** Always crash the activity on the **Critical Path** that has the **LOWEST cost slope** first.
3. Stop crashing when the target completion date is reached, or when all critical paths cannot be shortened further.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> A company is constructing a regional branch office. The activity schedule with immediate predecessors and durations is shown below:
>
> | Activity | Description | Predecessors | Duration (Weeks) |
> | :---: | :---: | :---: | :---: |
> | **A** | Site Clearance | None | 4 |
> | **B** | Foundation | A | 6 |
> | **C** | Framing & Walls | B | 8 |
> | **D** | Electrical Wiring | B | 4 |
> | **E** | Plumbing | B | 5 |
> | **F** | Interior Plaster | C | 6 |
> | **G** | Fixture Installation | D, E | 7 |
> | **H** | Final Painting & Cleanup | F, G | 3 |
>
> **Required:**  
> (a) Compute the Early Start (ES), Early Finish (EF), Late Start (LS), and Late Finish (LF) for all activities.  
> (b) Calculate the Total Float and Free Float for each activity.  
> (c) Identify the Critical Path and the minimum project completion duration.

---

### Step 1: Forward Pass (Early Start & Early Finish)

* **Activity A (Predecessor: None):**
  * `ES = 0`
  * `EF = 0 + 4 = 4`
* **Activity B (Predecessor: A):**
  * `ES = EF(A) = 4`
  * `EF = 4 + 6 = 10`
* **Activity C (Predecessor: B):**
  * `ES = EF(B) = 10`
  * `EF = 10 + 8 = 18`
* **Activity D (Predecessor: B):**
  * `ES = EF(B) = 10`
  * `EF = 10 + 4 = 14`
* **Activity E (Predecessor: B):**
  * `ES = EF(B) = 10`
  * `EF = 10 + 5 = 15`
* **Activity F (Predecessor: C):**
  * `ES = EF(C) = 18`
  * `EF = 18 + 6 = 24`
* **Activity G (Predecessors: D, E):**
  * `ES = MAX(EF(D), EF(E)) = MAX(14, 15) = 15`
  * `EF = 15 + 7 = 22`
* **Activity H (Predecessors: F, G):**
  * `ES = MAX(EF(F), EF(G)) = MAX(24, 22) = 24`
  * `EF = 24 + 3 = 27`

**Project Expected Duration = 27 Weeks.**

---

### Step 2: Backward Pass (Late Start & Late Finish)

Set final project finish: `LF(H) = EF(H) = 27`.

* **Activity H:**
  * `LF = 27`
  * `LS = 27 - 3 = 24`
* **Activity F (Successor: H):**
  * `LF = LS(H) = 24`
  * `LS = 24 - 6 = 18`
* **Activity G (Successor: H):**
  * `LF = LS(H) = 24`
  * `LS = 24 - 7 = 17`
* **Activity C (Successor: F):**
  * `LF = LS(F) = 18`
  * `LS = 18 - 8 = 10`
* **Activity D (Successor: G):**
  * `LF = LS(G) = 17`
  * `LS = 17 - 4 = 13`
* **Activity E (Successor: G):**
  * `LF = LS(G) = 17`
  * `LS = 17 - 5 = 12`
* **Activity B (Successors: C, D, E):**
  * `LF = MIN(LS(C), LS(D), LS(E)) = MIN(10, 13, 12) = 10`
  * `LS = 10 - 6 = 4`
* **Activity A (Successor: B):**
  * `LF = LS(B) = 4`
  * `LS = 4 - 4 = 0`

---

### Step 3: Complete Network Schedule & Float Analysis Table

| Activity | Duration | Early Start (ES) | Early Finish (EF) | Late Start (LS) | Late Finish (LF) | Total Float (`LS - ES`) | Free Float (`ES_succ - EF`) | Critical? |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **A** | 4 | 0 | 4 | 0 | 4 | **0** | `4 - 4 = 0` | **YES** |
| **B** | 6 | 4 | 10 | 4 | 10 | **0** | `10 - 10 = 0` | **YES** |
| **C** | 8 | 10 | 18 | 10 | 18 | **0** | `18 - 18 = 0` | **YES** |
| **D** | 4 | 10 | 14 | 13 | 17 | **3** | `15 - 14 = 1` | NO |
| **E** | 5 | 10 | 15 | 12 | 17 | **2** | `15 - 15 = 0` | NO |
| **F** | 6 | 18 | 24 | 18 | 24 | **0** | `24 - 24 = 0` | **YES** |
| **G** | 7 | 15 | 22 | 17 | 24 | **2** | `24 - 22 = 2` | NO |
| **H** | 3 | 24 | 27 | 24 | 27 | **0** | `27 - 27 = 0` | **YES** |

---

### Step 4: Summary of Project Findings
1. **Critical Path:** `A -> B -> C -> F -> H`
2. **Project Duration:** `4 + 6 + 8 + 6 + 3 = 27 Weeks`.
3. **Managerial Insights:**
   * Activity D has 3 weeks of total float (can start as late as week 13 without impacting the 27-week deadline).
   * Activity G has 2 weeks of total float.
   * Activities on the path `A-B-C-F-H` have zero float; any delay here delays the grand opening.

---

## 4. Exam Traps & Gotchas

1. **The Merge Trap (Forward Pass):**
   * When two activities converge into one successor (e.g. D and E entering G), students frequently take the average or the minimum.
   * **Rule:** You **MUST take the MAXIMUM** early finish (`MAX(14, 15) = 15`), because work on G cannot commence until *both* preceding activities are completely finished!
2. **The Burst Trap (Backward Pass):**
   * When an activity branches into multiple successors (e.g. B leading to C, D, and E), you **MUST take the MINIMUM** late start (`MIN(10, 13, 12) = 10`). Taking anything higher creates an impossible schedule for the tightest successor!
3. **PERT Variance Trap:**
   * Never sum standard deviations! Standard deviations are not additive.
   * You **MUST sum variances** along the critical path first (`sigma_proj^2 = sum(sigma_i^2)`), and only then take the square root (`sigma_proj = sqrt(sum)`).
