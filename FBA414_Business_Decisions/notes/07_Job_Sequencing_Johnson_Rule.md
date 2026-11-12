# FBA 414: Note 07 — Job Sequencing & Scheduling: Johnson's Rule
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 19)  
**Exam Focus:** Johnson’s Algorithm for $n$ Jobs on 2 Machines, Conversion for 3 Machines, Total Elapsed Time (Makespan), Idle Time Analysis.

---

## 1. The Core Intuition
In a manufacturing shop, multiple independent jobs arrive simultaneously, each requiring sequential processing on two or three distinct machines in a strict order (e.g., Turning on Machine 1, then Grinding on Machine 2).

The management problem is **Sequencing**: In what specific order should the jobs be processed to:
1. **Minimize the Total Elapsed Time (Makespan):** The total time from when the first job starts on Machine 1 until the last job leaves Machine 2.
2. **Minimize Idle Time:** Time during which machines are standing unused waiting for parts.

S. M. Johnson (1954) established the definitive, mathematically optimal scheduling rule.

---

## 2. The Step-by-Step Johnson's Algorithm ("The Recipe")

### Part A: Johnson’s Rule for $n$ Jobs on 2 Machines ($M_1 \rightarrow M_2$)

#### Step 1: Scan for the Global Minimum
* Examine the processing times of all unscheduled jobs on both machines.
* Identify the **smallest processing time** in the entire table.

#### Step 2: Placement Rule
* **If the minimum time occurs on Machine 1:**
  * Schedule that job **as EARLY as possible** (place it in the first available slot at the left end of the sequence).
* **If the minimum time occurs on Machine 2:**
  * Schedule that job **as LATE as possible** (place it in the last available slot at the right end of the sequence).

#### Step 3: Iterate
* Cross out the scheduled job from the table.
* Repeat Steps 1 and 2 for the remaining unscheduled jobs until all $n$ slots are filled.
* *(Tie-breaking: If a tie occurs on Machine 1, pick either. If a tie occurs on Machine 2, pick either. If the same minimum occurs on both Machine 1 for one job and Machine 2 for another job, place the M1 job first and the M2 job last).*

#### Step 4: Construct the Schedule (In-Out) Table
* For each job in the optimal sequence, calculate:
  * **Machine 1:** `Time In` and `Time Out = Time In + Processing Time`.
  * **Machine 2:**
    * `Time In = MAX( Machine 1 Time Out for this job, Machine 2 Time Out for previous job )`.
    * `Time Out = Time In + Processing Time`.
* **Total Elapsed Time (Makespan):** The final `Time Out` of the last job on Machine 2.
* **Idle Time on Machine 1:** `Makespan - Machine 1 Final Time Out`.
* **Idle Time on Machine 2:** Sum of all waiting periods before starting jobs.

---

### Part B: Extension to 3 Machines ($M_1 \rightarrow M_2 \rightarrow M_3$)

Direct Johnson's algorithm cannot be run on 3 machines unless at least one of the following two **feasibility conditions** is satisfied:
1. `MIN [ Processing time on M_1 ] >= MAX [ Processing time on M_2 ]`  
   **OR**
2. `MIN [ Processing time on M_3 ] >= MAX [ Processing time on M_2 ]`

#### The 3-Machine Procedure:
1. Check the two conditions. If at least one holds, proceed.
2. Convert the 3-machine problem into a fictitious 2-machine problem by defining two pseudo-machines:
   * **Machine G:** `Time(G) = Time(M_1) + Time(M_2)`
   * **Machine H:** `Time(H) = Time(M_2) + Time(M_3)`
3. Apply standard 2-machine Johnson’s rule to pseudo-machines **G** and **H** to find the optimal sequence.
4. Build the final In-Out table using the **original processing times** of $M_1$, $M_2$, and $M_3$ to find the true Makespan.

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Five production batches (Jobs A, B, C, D, E) must be processed through two consecutive departments: **Drilling (Machine 1)** and **Polishing (Machine 2)**. The processing times (in hours) are:
>
> | Job | Drilling ($M_1$) | Polishing ($M_2$) |
> | :---: | :---: | :---: |
> | **A** | 7 | 4 |
> | **B** | 3 | 8 |
> | **C** | 11 | 9 |
> | **D** | 5 | 12 |
> | **E** | 12 | 3 |
>
> **Required:**  
> (a) Determine the optimal processing sequence using Johnson’s Rule.  
> (b) Construct the complete In-Out schedule table.  
> (c) Calculate the Total Elapsed Time (Makespan) and total idle time for both machines.

---

### Step 1: Execute Johnson's Rule Sequence Selection

We have 5 slots: `[ 1st,  2nd,  3rd,  4th,  5th ]`

* **Iteration 1:**
  * Find the global minimum across all times: Minimum is **3 hours**, which occurs for **Job B** on $M_1$ and **Job E** on $M_2$.
  * Job B is on $M_1$ -> Place Job B **as early as possible** (Slot 1).
  * Job E is on $M_2$ -> Place Job E **as late as possible** (Slot 5).
  * Current Sequence: `[ B,  ____,  ____,  ____,  E ]`
  * Remaining Jobs: `A, C, D`.

* **Iteration 2:**
  * Minimum among remaining jobs: **4 hours** for **Job A** on $M_2$.
  * Since it is on $M_2$, place Job A **as late as possible** in the remaining slots (Slot 4).
  * Current Sequence: `[ B,  ____,  ____,  A,  E ]`
  * Remaining Jobs: `C, D`.

* **Iteration 3:**
  * Minimum among remaining: **5 hours** for **Job D** on $M_1$.
  * Since it is on $M_1$, place Job D **as early as possible** in the remaining slots (Slot 2).
  * Current Sequence: `[ B,  D,  ____,  A,  E ]`
  * Only Job C remains -> Place Job C in Slot 3.

**Final Optimal Sequence:**  
`B -> D -> C -> A -> E`

---

### Step 2: Construct the In-Out Schedule Table

Using the sequence `B -> D -> C -> A -> E`:

| Job in Sequence | Drilling ($M_1$) Time In | Drilling ($M_1$) Time Out | Polishing ($M_2$) Time In | Polishing ($M_2$) Time Out | Idle Time on $M_2$ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **B** | 0 | `0 + 3 = 3` | 3 | `3 + 8 = 11` | 3 (from 0 to 3) |
| **D** | 3 | `3 + 5 = 8` | `max(8, 11) = 11` | `11 + 12 = 23` | 0 |
| **C** | 8 | `8 + 11 = 19` | `max(19, 23) = 23` | `23 + 9 = 32` | 0 |
| **A** | 19 | `19 + 7 = 26` | `max(26, 32) = 32` | `32 + 4 = 36` | 0 |
| **E** | 26 | `26 + 12 = 38` | `max(38, 36) = 38` | `38 + 3 = 41` | 2 (from 36 to 38) |

---

### Step 3: Summary of Results

1. **Total Elapsed Time (Makespan):**
   `Makespan = 41 Hours` (The completion time of Job E on Machine 2).
2. **Total Processing Time on Machine 1:**
   `3 + 5 + 11 + 7 + 12 = 38 Hours`.
3. **Idle Time on Machine 1:**
   `Makespan - Total M_1 Time = 41 - 38 = 3 Hours`  
   *(Machine 1 stands idle from hour 38 to 41 while Machine 2 finishes Job E)*.
4. **Total Processing Time on Machine 2:**
   `8 + 12 + 9 + 4 + 3 = 36 Hours`.
5. **Idle Time on Machine 2:**
   `Makespan - Total M_2 Time = 41 - 36 = 5 Hours`  
   *(3 hours at the start waiting for Job B + 2 hours between hours 36 and 38 waiting for Job E)*.

---

## 4. Exam Traps & Gotchas

1. **The Machine 2 Time In Rule:**
   * Students often mistakenly set `M_2 Time In` equal to `M_1 Time Out`.
   * **Rule:** Machine 2 cannot start a job until:
     1. Machine 1 has finished that job, **AND**
     2. Machine 2 has finished the *previous* job!
   * Therefore: `M_2 Time In = MAX [ M_1 Time Out of current job, M_2 Time Out of previous job ]`.
2. **The 3-Machine Condition Trap:**
   * Never combine 3 machines into `G` and `H` without first stating the condition:
     `min(M_1) >= max(M_2)` OR `min(M_3) >= max(M_2)`.
   * In a written exam, stating this condition earns 2 easy marks before doing any calculations!

