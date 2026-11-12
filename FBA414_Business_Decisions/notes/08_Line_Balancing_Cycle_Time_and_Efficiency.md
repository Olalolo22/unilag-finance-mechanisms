# FBA 414: Note 08 — Assembly Line Balancing: Cycle Time & Line Efficiency
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 20)  
**Exam Focus:** Cycle Time Determination, Theoretical Minimum Stations, Ranked Positional Weight (RPW) Heuristic, Line Efficiency, Balance Delay.

---

## 1. The Core Intuition
In mass-production assembly lines (such as automotive, electronics, or beverage bottling plants), an unfinished product moves continuously along a conveyor through a sequence of physical workstations. At each station, human workers or robotic arms perform specific sub-assembly tasks.

The core engineering and managerial challenge is **Line Balancing**: How do we group dozens of tiny discrete tasks into workstations such that:
1. Every task’s **precedence requirements** (technological order) are strictly satisfied.
2. The total work assigned to any single workstation does not exceed the line’s **Cycle Time** (the pace of the conveyor belt).
3. Total workstation **idle time is minimized**, maximizing line efficiency.

---

## 2. The Core Formulas & The RPW Algorithm ("The Recipe")

### Part A: Fundamental Line Balancing Equations

1. **Cycle Time (`C`):**
   The maximum permissible time the product spends at each workstation:
   `C = Available Operating Time per Day / Desired Production Output per Day`
   *(Units: Minutes per unit, or Seconds per unit).*

2. **Total Work Content (`T_wc`):**
   The sum of all individual elemental task times:
   `T_wc = SUM [ t_i ]`

3. **Theoretical Minimum Number of Workstations (`N_min`):**
   `N_min = T_wc / C`
   * **MANDATORY EXAM RULE:** Always **round UP** to the next whole integer, even if the decimal is small (e.g., `3.15` stations must be rounded up to `4` stations).

4. **Line Efficiency (`E`):**
   The percentage of total workstation time spent performing actual productive work:
   `Line Efficiency (%) = [ T_wc / (N_actual * C) ] * 100%`

5. **Balance Delay (`BD`):**
   The percentage of total line capacity wasted as idle time:
   `Balance Delay (%) = 100% - Line Efficiency (%)`
   `Balance Delay (%) = [ (N_actual * C - T_wc) / (N_actual * C) ] * 100%`

---

### Part B: The Ranked Positional Weight (RPW) Heuristic (Helgeson-Birnie Method)

When grouping tasks, trial-and-error fails for large problems. The standard algorithm taught and tested at UNILAG is **RPW**:

* **Step 1 (Construct Precedence Diagram):** Draw the network of tasks showing which activities must precede others.
* **Step 2 (Calculate Positional Weight for Every Task):**
  * For each task `i`, compute its **Positional Weight (`PW_i`)**:
    `PW_i = Task Time (t_i) + SUM [ Task Times of ALL downstream tasks that follow task i ]`
  * *(The positional weight represents the total cumulative work dependent on task `i`).*
* **Step 3 (Rank Tasks):** List all tasks in **descending order** of their Positional Weights (highest `PW` at the top).
* **Step 4 (Assign Tasks to Workstations):**
  * Start at Workstation 1.
  * Proceed down the ranked list and assign the highest-ranked task that:
    1. Has had all its **immediate predecessors already assigned**, and
    2. Has a task time `t_i` that does not cause total station time to exceed Cycle Time `C`.
  * When no further tasks can fit into Workstation 1 without exceeding `C`, close Workstation 1 and open Workstation 2.
  * Repeat until all tasks are fully assigned.
* **Step 5 (Calculate Metrics):** Compute the actual number of stations `N_actual`, Line Efficiency, and Balance Delay.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> An appliance assembly line operates **8 hours per day** (480 minutes) and is designed to produce **120 microwave ovens per day**. The assembly process consists of eight distinct tasks with the following times and precedence relationships:
>
> | Task | Description | Immediate Predecessors | Task Time ($t_i$, Minutes) |
> | :---: | :---: | :---: | :---: |
> | **A** | Assemble chassis | None | 1.8 |
> | **B** | Install transformer | A | 1.2 |
> | **C** | Install magnetron | A | 1.5 |
> | **D** | Attach wiring harness | B | 0.8 |
> | **E** | Mount control panel | C | 1.0 |
> | **F** | Install turntable motor | D, E | 1.4 |
> | **G** | Attach outer casing | F | 1.1 |
> | **H** | Final safety test & pack | G | 1.2 |
>
> **Required:**  
> (a) Calculate the required Cycle Time in minutes.  
> (b) Compute the Theoretical Minimum Number of Workstations.  
> (c) Apply the Ranked Positional Weight (RPW) heuristic to balance the line.  
> (d) Calculate the Line Efficiency and the Balance Delay.

---

### Step 1: Preliminary Calculations

1. **Cycle Time (`C`):**
   `Available Time = 8 hours * 60 minutes = 480 minutes per day`
   `Target Output = 120 units per day`
   `C = 480 / 120 = 4.0 Minutes per unit`

2. **Total Work Content (`T_wc`):**
   `T_wc = 1.8 + 1.2 + 1.5 + 0.8 + 1.0 + 1.4 + 1.1 + 1.2 = 10.0 Minutes`

3. **Theoretical Minimum Workstations (`N_min`):**
   `N_min = T_wc / C = 10.0 / 4.0 = 2.5 stations`  
   Round up to next integer: **`N_min = 3 Workstations`**.

---

### Step 2: Compute Positional Weights (RPW)

* **Task H:** Downstream = None -> `PW(H) = 1.2`
* **Task G:** Followed by H -> `PW(G) = 1.1 + 1.2 = 2.3`
* **Task F:** Followed by G, H -> `PW(F) = 1.4 + 1.1 + 1.2 = 3.7`
* **Task E:** Followed by F, G, H -> `PW(E) = 1.0 + 3.7 = 4.7`
* **Task D:** Followed by F, G, H -> `PW(D) = 0.8 + 3.7 = 4.5`
* **Task C:** Followed by E, F, G, H -> `PW(C) = 1.5 + 1.0 + 3.7 = 6.2`
* **Task B:** Followed by D, F, G, H -> `PW(B) = 1.2 + 0.8 + 3.7 = 5.7`
* **Task A:** Followed by all downstream tasks -> `PW(A) = 1.8 + (all others) = 10.0`

#### RPW Ranking Table:

| Task | Task Time ($t_i$) | Immediate Predecessors | Positional Weight (`PW`) | Rank |
| :---: | :---: | :---: | :---: | :---: |
| **A** | 1.8 | None | **10.0** | 1 |
| **C** | 1.5 | A | **6.2** | 2 |
| **B** | 1.2 | A | **5.7** | 3 |
| **E** | 1.0 | C | **4.7** | 4 |
| **D** | 0.8 | B | **4.5** | 5 |
| **F** | 1.4 | D, E | **3.7** | 6 |
| **G** | 1.1 | F | **2.3** | 7 |
| **H** | 1.2 | G | **1.2** | 8 |

---

### Step 3: Workstation Assignments (Cycle Time Limit $C = 4.0$ min)

#### Workstation 1:
* Assign **Task A** (Time = 1.8; Cumulative = 1.8 <= 4.0; Unused = 2.2).
* Next highest eligible task is **C** (Time = 1.5; Predecessor A is done; Cumulative = 1.8 + 1.5 = 3.3 <= 4.0; Unused = 0.7).
* Next highest is B (Time = 1.2 > 0.7; cannot fit).
* Tasks E, D, F, G, H either exceed 0.7 or have unmet predecessors.
* **Close Workstation 1:** Total Time = **3.3 minutes**; Idle Time = `4.0 - 3.3 = 0.7 minutes`.

#### Workstation 2:
* Start fresh with remaining capacity = 4.0 minutes.
* Assign **Task B** (Time = 1.2; Predecessor A done; Cumulative = 1.2 <= 4.0; Unused = 2.8).
* Assign **Task E** (Time = 1.0; Predecessor C done; Cumulative = 1.2 + 1.0 = 2.2 <= 4.0; Unused = 1.8).
* Assign **Task D** (Time = 0.8; Predecessor B done; Cumulative = 2.2 + 0.8 = 3.0 <= 4.0; Unused = 1.0).
* Next is Task F (requires D and E; both are done! But Time = 1.4 > 1.0 unused; cannot fit).
* **Close Workstation 2:** Total Time = **3.0 minutes**; Idle Time = `4.0 - 3.0 = 1.0 minutes`.

#### Workstation 3:
* Start fresh with remaining capacity = 4.0 minutes.
* Assign **Task F** (Time = 1.4; Cumulative = 1.4 <= 4.0; Unused = 2.6).
* Assign **Task G** (Time = 1.1; Predecessor F done; Cumulative = 1.4 + 1.1 = 2.5 <= 4.0; Unused = 1.5).
* Assign **Task H** (Time = 1.2; Predecessor G done; Cumulative = 2.5 + 1.2 = 3.7 <= 4.0; Unused = 0.3).
* All tasks assigned!
* **Close Workstation 3:** Total Time = **3.7 minutes**; Idle Time = `4.0 - 3.7 = 0.3 minutes`.

---

### Step 4: Final Line Balancing Summary Table

| Workstation | Assigned Tasks | Total Station Time (min) | Station Idle Time (`4.0 - Time`) |
| :---: | :---: | :---: | :---: |
| **WS 1** | A, C | 3.3 min | 0.7 min |
| **WS 2** | B, E, D | 3.0 min | 1.0 min |
| **WS 3** | F, G, H | 3.7 min | 0.3 min |
| **TOTAL** | **8 Tasks** | **10.0 min** | **2.0 min** |

* Actual Stations Used: `N_actual = 3` (matches the theoretical minimum `N_min = 3`!).

---

### Step 5: Calculate Efficiency & Balance Delay

1. **Line Efficiency (`E`):**
   `E = [ T_wc / (N_actual * C) ] * 100%`  
   `E = [ 10.0 / (3 * 4.0) ] * 100% = [ 10.0 / 12.0 ] * 100% = 83.33%`

2. **Balance Delay (`BD`):**
   `BD = 100% - 83.33% = 16.67%`  
   *(Or using idle time: `[ 2.0 / 12.0 ] * 100% = 16.67%`)*.

---

## 4. Exam Traps & Gotchas

1. **Rounding `N_min` Down:**
   * If `N_min = 2.1`, rounding down to 2 is physically impossible—2 stations with cycle time 4.0 can only do 8.0 minutes of work, leaving 2 minutes unassigned! **Always round up to the next integer**.
2. **Precedence Violations:**
   * Students frequently assign Task F to Workstation 2 because it has a high rank, forgetting that Task F requires *both* D and E to be completed first!
3. **Bottleneck Station:**
   * The station with the highest total time is the **bottleneck station** (here, Workstation 3 at 3.7 minutes). The line can never produce faster than its bottleneck station.

