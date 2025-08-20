# 📘 Chapter 1: Introduction to Machine Learning (Tom Mitchell)

## 1. Why Machine Learning?

* Since the beginning of computing, people wondered if computers could **learn** instead of just being programmed.
* If computers could learn from experience, they could:

  * Discover effective medical treatments from patient data.
  * Help homes optimize energy use.
  * Adapt to user interests (like a smart news recommender).
* Machine learning already outperforms traditional methods in some domains:

  * **Speech recognition**
  * **Credit card fraud detection**
  * **Driving autonomous vehicles**
  * **Game playing** (e.g., backgammon, checkers)

👉 Takeaway: Machine learning = computers improving automatically with experience, useful for tasks where programming explicit rules is too complex.

---

## 2. What is Learning? (Formal Definition)

Mitchell’s definition:

> A computer program learns from **experience (E)** with respect to some class of **tasks (T)** and a **performance measure (P)**, if its performance at tasks in T, as measured by P, improves with experience E.

### Example:

* **Task (T):** Playing checkers
* **Performance measure (P):** % of games won
* **Experience (E):** Playing many practice games against itself

👉 To define a well-posed learning problem, you must specify **Task, Performance, Experience**.

---

## 3. Designing a Learning System (Checkers Example 🏁)

Let’s say we want to build a program to play checkers.

### Step 1: Choose the Training Experience

* Options:

  * **Direct feedback**: system sees a board + correct move.
  * **Indirect feedback**: system only knows the game’s final result (win/lose).
* Training can be:

  * Teacher-provided.
  * Learner-driven (asking for clarification).
  * Self-play (program generates its own games).
* ⚠️ Danger: if training data ≠ test conditions, performance may fail (e.g., training only on self-play may miss human strategies).

---

### Step 2: Choose the Target Function

* Naïve choice: **ChooseMove(board) → best move**.

  * Hard to learn directly.
* Better choice: **Evaluation function V(board) → score**

  * Assigns a value to a board state (good, bad, neutral).
  * Then pick the move leading to the best-scoring board.

👉 Learning is often about **approximating a function**.

---

### Step 3: Choose Representation

* How to represent V(board)?

  * A huge table of all states? → Impossible.
  * Logical rules? Polynomials? Neural networks?
* Simplified version: Linear function of features.
  Example features:

  * number of black pieces
  * number of red pieces
  * number of black kings
  * number of red kings
  * number of threatened pieces, etc.

V(b) = w₀ + w₁x₁ + w₂x₂ + … + w₆x₆

👉 Learning reduces to **finding the weights** (w’s).

---

### Step 4: Choose Learning Algorithm

* Need training examples: (board, value).
* Problem: we only know the **final game result**, not intermediate board values.
* Trick: Estimate intermediate value using successor states (bootstrapping idea).
* **LMS rule (Least Mean Squares):**

  * Adjust weights a little each time to reduce error.
  * This is basically **stochastic gradient descent**.

---

### Step 5: Final System (Modules)

The checkers learner has four parts (Figure 1.1):

1. **Performance System** – plays the game.
2. **Critic** – evaluates game traces, produces training examples.
3. **Generalizer** – learns a function from examples (e.g., LMS algorithm).
4. **Experiment Generator** – decides what training experiences to create (e.g., self-play).

👉 Most ML systems can be described using these four roles.

---

## 4. Perspectives on Machine Learning

* Learning = **searching hypothesis space**.

  * In checkers: all linear functions of 6 features.
* Goal: find a hypothesis consistent with training data.
* Different algorithms explore different hypothesis spaces:

  * Decision trees
  * Neural networks
  * Probabilistic models
  * Rule-based systems

---

## 5. Key Issues in ML (Big Questions)

* What algorithms work best for which problems?
* How much data is enough?
* How can prior knowledge help learning?
* How to choose or generate training data effectively?
* How to pick good target functions?
* How to improve representations automatically?

---

## 6. Chapter Summary

* Machine learning = programs improving performance through experience.
* Must specify **Task, Performance measure, Experience**.
* Designing involves choosing:

  * Training experience
  * Target function
  * Representation
  * Learning algorithm
* Learning is search in hypothesis space.
* Applications span data mining, dynamic adaptation, and poorly understood domains.

---

✅ **Teaching Note:**
This chapter is mainly about **framing ML problems** — how to formalize learning, think in terms of task-performance-experience, and design systems. The checkers example is used to illustrate the full design cycle.

---


