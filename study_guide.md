# 📘 Chapter 1: Introduction to Machine Learning

---

## 1. What is Machine Learning?

* **Goal:** Programs that improve automatically with experience.

* **Definition (Mitchell, 1997):**

  > A program learns from **experience (E)**, with respect to **tasks (T)** and a **performance measure (P)**, if its performance at T, measured by P, improves with E.

* **Applications:**

  * Speech recognition
  * Fraud detection
  * Self-driving cars
  * Games (checkers, backgammon)
  * Data mining (medical, finance, astronomy)

---

## 2. Well-Posed Learning Problems

* Need to specify:

  1. **Task (T)**
  2. **Performance measure (P)**
  3. **Training experience (E)**

**Example – Checkers**

* T: Playing checkers
* P: % of games won
* E: Self-play games

---

## 3. Designing a Learning System (Checkers Example 🏁)

### Step 1 – Training Experience

* **Direct feedback** (easier): correct move for each state.
* **Indirect feedback** (harder): only final game outcome (win/lose).
* **Danger:** Training ≠ test distribution → poor generalization.

### Step 2 – Target Function

* Option A: **ChooseMove(board) → best move** (hard).
* Option B: **V(board) → numeric score** (better).

  * Higher = better board state.
  * Choose move → leads to best successor state.

### Step 3 – Representation

* **Linear function of features:**

  ```
  V(b) = w0 + w1x1 + w2x2 + … + w6x6
  ```

  * x1: # black pieces
  * x2: # red pieces
  * x3: # black kings
  * x4: # red kings
  * x5: black pieces threatened
  * x6: red pieces threatened

👉 Learning reduces to **finding weights (w’s).**

### Step 4 – Learning Algorithm

* **Need examples (b, Vtrain(b))**.
* Problem: only know final result → estimate intermediate values:

  ```
  Vtrain(b) ≈ V(successor(b))
  ```
* **LMS rule (Least Mean Squares):**

  * For each training example:

    ```
    wi ← wi + η (Vtrain(b) – V(b)) xi
    ```

    where η = learning rate.
* Equivalent to **stochastic gradient descent**.

---

## 4. Final Design – 4 Modules

```
[ Experiment Generator ] → picks new problems (e.g., self-play)
            ↓
[ Performance System ] → plays checkers using learned V
            ↓
[ Critic ] → evaluates games, produces training examples
            ↓
[ Generalizer ] → learns hypothesis (updates weights)
```

---

## 5. Perspectives on Machine Learning

* **Learning = search** through hypothesis space.
* Different algorithms = different hypothesis representations:

  * Linear functions
  * Decision trees
  * Neural networks
  * Probabilistic models

---

## 6. Key Issues in ML

* Which algorithms converge?
* How much training data is enough?
* How to use prior knowledge?
* How to pick/generate training data?
* How to represent target functions?
* Can representation evolve automatically?

---

## 7. Chapter Summary

* Machine learning = **experience → improved performance**.
* Need: **Task, Performance, Experience**.
* Design involves:

  1. Training experience
  2. Target function
  3. Representation
  4. Algorithm
* Learning = **hypothesis space search**.
* Applications: data mining, adaptation, complex tasks.

---

✅ **Formulas to Remember**

* **Linear evaluation function:**

  ```
  V(b) = w0 + Σ wi xi
  ```
* **LMS weight update rule:**

  ```
  wi ← wi + η (Vtrain(b) – V(b)) xi
  ```

---

✅ **Quick Diagram (Learning Loop)**

```
Training Experience → Critic → Training Examples
                                ↓
Experiment Generator → Performance System → Game Trace
                                ↓
                        Generalizer → Hypothesis (f)
```

---

