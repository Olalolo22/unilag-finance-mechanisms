# FBA 414: Note 04 — Game Theory: Pure, Mixed Strategies & Dominance
**Course:** Analysis for Business Decisions / Management Science  
**Recommended Reference:** T. Lucey, *Quantitative Techniques* (6th ed., Chapter 16)  
**Exam Focus:** Two-Person Zero-Sum Games, Saddle Point Identification, The Dominance Principle, $2 \times 2$ Algebraic Odds Method, Expected Value of the Game.

---

## 1. The Core Intuition
**Game Theory** models strategic decision-making where two or more rational competitors (players) face interdependent payoffs. In FBA 414, the curriculum focuses on **Two-Person Zero-Sum Games**:
* **Two-Person:** Exactly two competing entities (e.g., Firm A vs. Firm B).
* **Zero-Sum:** What one player gains, the other player loses exactly (`Gain of Player A + Loss of Player B = 0`).
* **Matrix Convention:** Numbers in the payoff matrix represent **payoffs to the Row Player (Player A)**:
  * Positive numbers = Player A wins / Player B pays.
  * Negative numbers = Player A pays / Player B wins.

A player chooses strategies under the conservative assumption that the opponent is intelligent and will play to minimize their advantage.

---

## 2. The Step-by-Step Algorithm ("The Recipe")

### Step 1: Check for a Saddle Point (Pure Strategy Test)
Always test for a saddle point before doing any algebra!
1. **Row Minima (Player A's Maximin):** Find the minimum value in each row. From these minima, select the **maximum** value. This is the **Maximin**.
2. **Column Maxima (Player B's Minimax):** Find the maximum value in each column. From these maxima, select the **minimum** value. This is the **Minimax**.
3. **Decision Rule:**
   * **If `Maximin = Minimax`:** A **Saddle Point** exists.
     * The game is **strictly determined**.
     * Both players play pure strategies corresponding to that saddle point cell.
     * **Value of the Game (`V`)** equals the saddle point value. Stop!
   * **If `Maximin != Minimax`:** No saddle point exists. The players must use **Mixed Strategies** (randomizing actions with specific probabilities). Proceed to Step 2.

---

### Step 2: Matrix Reduction using the Dominance Principle
If the matrix is larger than $2 \times 2$ (e.g., $3 \times 3$ or $3 \times 4$), reduce its dimensions using dominance rules:

* **Row Dominance Rule (Player A maximizes payoff):**
  * If every element in Row $i$ is less than or equal to the corresponding element in Row $k$ (`Row_i <= Row_k`), then **Row $i$ is dominated** by Row $k$.
  * **Action:** Delete Row $i$ completely (Player A will never play an inferior strategy).
* **Column Dominance Rule (Player B minimizes payoff):**
  * If every element in Column $j$ is greater than or equal to the corresponding element in Column $m$ (`Col_j >= Col_m`), then **Column $j$ is dominated** by Column $m$.
  * **Action:** Delete Column $j$ completely (Player B will never allow Player A to earn higher payoffs).
* **Average Dominance:** A row (or column) can also be deleted if it is dominated by the average of two other rows (or columns).

Repeat until the matrix is reduced to a **$2 \times 2$ matrix**.

---

### Step 3: Solving a $2 \times 2$ Mixed Strategy Game (Algebraic Odds Method)
For a $2 \times 2$ payoff matrix without a saddle point:

```text
                  Player B
              Strategy 1   Strategy 2
Player A  1 [     a            b     ]
          2 [     c            d     ]
```

#### 1. Player A's Probabilities (`p_1, p_2`):
* Take the absolute difference of Row 2: `|c - d|` -> Assign as weight to Strategy 1.
* Take the absolute difference of Row 1: `|a - b|` -> Assign as weight to Strategy 2.
* Total Row Weight: `W_row = |c - d| + |a - b|`
* Probabilities:
  `p_1 = |c - d| / W_row`
  `p_2 = |a - b| / W_row`  *(Note: `p_1 + p_2 = 1`)*

#### 2. Player B's Probabilities (`q_1, q_2`):
* Take the absolute difference of Column 2: `|b - d|` -> Assign as weight to Strategy 1.
* Take the absolute difference of Column 1: `|a - c|` -> Assign as weight to Strategy 2.
* Total Column Weight: `W_col = |b - d| + |a - c|`
* Probabilities:
  `q_1 = |b - d| / W_col`
  `q_2 = |a - c| / W_col`  *(Note: `q_1 + q_2 = 1`)*

#### 3. Expected Value of the Game (`V`):
`V = (a * d - b * c) / ( (a + d) - (b + c) )`

Alternatively, calculate by expected payoff:
`V = p_1 * a + p_2 * c` (against B's Strategy 1).

---

## 3. Comprehensive Worked UNILAG Exam Problem

### Problem Statement:
> Two competing commercial banks, **Alpha Bank (Player A)** and **Zenith Bank (Player B)**, are competing for retail market share by launching marketing campaigns across three media channels: (1) Television, (2) Radio, and (3) Digital/Social Media.  
> The payoff matrix representing Alpha Bank's percentage market share gain (+) or loss (-) is:
>
> ```text
>                    Zenith Bank (Player B)
>                   B_1 (TV)   B_2 (Radio)   B_3 (Digital)
> Alpha Bank   A_1 [    3           -1             4       ]
> (Player A)   A_2 [    6            7            -2       ]
>              A_3 [    4            2             1       ]
> ```
>
> **Required:**  
> (a) Check if a saddle point exists.  
> (b) Use the dominance principle to reduce the game to a $2 \times 2$ matrix.  
> (c) Determine the optimal mixed strategies for both banks.  
> (d) Calculate the expected value of the game.

---

### Step 1: Test for a Saddle Point

```text
                  B_1    B_2    B_3     Row Minimum
          A_1      3     -1      4         -1
          A_2      6      7     -2         -2
          A_3      4      2      1          1  <-- MAXIMIN = 1
---------------------------------------------
Col Maximum        6      7      4
                         MINIMAX = 4 (under B_3) or 6 (under B_1) -> Min = 4
```

* **Maximin (Player A):** `max(-1, -2, 1) = 1` (Strategy `A_3`)
* **Minimax (Player B):** `min(6, 7, 4) = 4` (Strategy `B_3`)
* Since `Maximin (1) != Minimax (4)`, **NO saddle point exists**.  
  The banks must play mixed strategies.

---

### Step 2: Apply the Dominance Principle

Let's examine columns (Zenith Bank wants smaller numbers):
* Compare **Column B_1** `[3, 6, 4]` and **Column B_3** `[4, -2, 1]`: No complete dominance.
* Compare **Row A_1** and **Row A_3**:
  * Row A_1 = `[ 3, -1, 4 ]`
  * Row A_3 = `[ 4,  2, 1 ]` -> Neither strictly dominates.
* What about an average of rows?
  * Average of Row A_1 and Row A_2:
    * Col 1: `(3 + 6) / 2 = 4.5` (beats Row A_3's `4`)
    * Col 2: `(-1 + 7) / 2 = 3.0` (beats Row A_3's `2`)
    * Col 3: `(4 + -2) / 2 = 1.0` (equals Row A_3's `1`)
  * Since the average of `(A_1, A_2)` provides payoffs of `[ 4.5, 3.0, 1.0 ]`, which are greater than or equal to Row A_3 `[ 4, 2, 1 ]`, **Row A_3 is dominated by the average of A_1 and A_2!**
  * **Delete Row A_3.**

Matrix becomes:
```text
             B_1    B_2    B_3
      A_1     3     -1      4
      A_2     6      7     -2
```

Now examine columns (Player B deletes columns with larger values):
* Compare **Column B_1** `[3, 6]` and **Column B_2** `[-1, 7]`: No dominance.
* What about an average of Column B_1 and Column B_3?
  * Average of B_1 and B_3:
    * Row 1: `(3 + 4) / 2 = 3.5`
    * Row 2: `(6 + -2) / 2 = 2.0`
* Notice Column B_2 has entries `[-1, 7]`. In Row 2, `7` is very large!
* Player B wants to minimize. In Row 2, B_2 gives Alpha Bank `+7`, which is terrible for Zenith Bank.
* Can Column B_1 dominate Column B_2?
  * If Zenith chooses a mix of B_2 and B_3:
    * Let's test standard dominance directly.
    * In standard UNILAG past questions, dominance is usually direct:
    * If `B_1` is dominated by a mix of `B_2` and `B_3`:
      Let `q * (-1) + (1-q) * 4 <= 3`  ===> `-5*q + 4 <= 3` ===> `5*q >= 1` ===> `q >= 0.2`
      Let `q * 7 + (1-q) * (-2) <= 6`  ===> `9*q - 2 <= 6`  ===> `9*q <= 8` ===> `q <= 0.88`
      Choosing `q = 0.5`: `0.5*(-1) + 0.5*(4) = 1.5 < 3` and `0.5*(7) + 0.5*(-2) = 2.5 < 6`.
    * Both entries `[1.5, 2.5]` are strictly smaller than Column B_1 `[3, 6]`.
    * Therefore, **Column B_1 is dominated by the convex combination of B_2 and B_3!**
    * **Delete Column B_1.**

Reduced $2 \times 2$ Matrix:
```text
                   Zenith Bank
                  B_2        B_3
Alpha     A_1 [   -1          4   ]
Bank      A_2 [    7         -2   ]
```

---

### Step 3: Solve the $2 \times 2$ Game

#### 1. Alpha Bank's Probabilities (`p_1, p_2`):
* Row 2 Difference: `|7 - (-2)| = |9| = 9` -> Weight for `A_1`
* Row 1 Difference: `|-1 - 4| = |-5| = 5` -> Weight for `A_2`
* Total Weight: `9 + 5 = 14`
* Probabilities:
  * `p_1 = 9 / 14` (Play Strategy `A_1` 64.3% of the time)
  * `p_2 = 5 / 14` (Play Strategy `A_2` 35.7% of the time)
  * `p_3 = 0` (Never play `A_3`)

#### 2. Zenith Bank's Probabilities (`q_2, q_3`):
* Column 2 (B_3) Difference: `|4 - (-2)| = |6| = 6` -> Weight for `B_2`
* Column 1 (B_2) Difference: `|-1 - 7| = |-8| = 8` -> Weight for `B_3`
* Total Weight: `6 + 8 = 14`
* Probabilities:
  * `q_1 = 0` (Never play `B_1`)
  * `q_2 = 6 / 14 = 3 / 7` (Play `B_2` 42.9% of the time)
  * `q_3 = 8 / 14 = 4 / 7` (Play `B_3` 57.1% of the time)

---

### Step 4: Value of the Game (`V`)
Using the analytical formula:
`V = (a * d - b * c) / ( (a + d) - (b + c) )`
* `a = -1,  b = 4,  c = 7,  d = -2`
* `a * d = (-1) * (-2) = 2`
* `b * c = 4 * 7 = 28`
* `Numerator = 2 - 28 = -26`
* `a + d = (-1) + (-2) = -3`
* `b + c = 4 + 7 = 11`
* `Denominator = (-3) - 11 = -14`
* `V = -26 / -14 = 13 / 7 = +1.857%`

**Interpretation:** Alpha Bank can guarantee an expected market share gain of **1.86%**, regardless of Zenith Bank's counter-strategy.

---

## 4. Exam Traps & Gotchas

1. **Skipping the Saddle Point Test:**
   * Always write down the `Maximin` and `Minimax` first. If they are equal, you will get an immediate 10/10 in 60 seconds without doing any fraction arithmetic!
2. **Reversing Row vs. Column Dominance:**
   * *Row rule:* Delete the **SMALLER** row (Player A wants big payoffs).
   * *Column rule:* Delete the **LARGER** column (Player B wants small payoffs).
3. **Fair Game Definition:**
   * A game is defined as **fair** if and only if the Value of the Game is exactly zero (`V = 0`).
   * If `V > 0`, the game is biased in favor of Player A (Row player).
   * If `V < 0`, the game is biased in favor of Player B (Column player).
