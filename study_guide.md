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

# 📘 Study Guide: Chapter 3 — Decision Tree Learning

---

## 🌳 1. What is Decision Tree Learning?

* **Definition**: A method for approximating **discrete-valued target functions** using a tree structure.
* **Representation**:

  * Each **internal node** → tests an attribute.
  * Each **branch** → possible value of that attribute.
  * Each **leaf** → classification result (Yes/No, category label, etc.).
* **Readable**: Can be converted into a set of **if–then rules**.
* **Use cases**: medical diagnosis, credit risk, equipment fault detection.

🔎 Example: *PlayTennis* dataset (attributes: Outlook, Humidity, Wind… → target: PlayTennis).

---

## 🎯 2. When to Use Decision Trees (Appropriate Problems)

* Instances are **attribute-value pairs** (e.g., Humidity = High).
* Target function has **discrete output values** (e.g., Yes/No).
* **Disjunctive concepts** possible (OR-combinations of conditions).
* **Noise tolerant** → can handle misclassified or missing data.
* Works well for **classification problems**.

---

## ⚙️ 3. The ID3 Algorithm (Core Decision Tree Algorithm)

* **Strategy**: Top-down, greedy search for the best attribute at each node.
* **Steps**:

  1. Start with all training examples at root.
  2. Pick the attribute with **highest Information Gain**.
  3. Split dataset on that attribute.
  4. Recurse on each branch until:

     * All examples at node are of the same class (pure), or
     * No attributes remain.

📌 **Key Definitions**:

* **Entropy** (measure of impurity):

  $$
  Entropy(S) = -p_+ \log_2(p_+) - p_- \log_2(p_-)
  $$

  * 0 → pure (all same class).
  * 1 → mixed (50/50).

* **Information Gain** (measure of attribute usefulness):

  $$
  Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \, Entropy(S_v)
  $$

  * Pick attribute with **highest gain**.

✅ Example (PlayTennis):

* Best root attribute = **Outlook** (highest info gain).

---

## 🔍 4. Hypothesis Space Search

* ID3 searches the space of **all possible decision trees**.
* Expressive enough for any finite discrete function.
* Uses **greedy, hill-climbing search** (no backtracking).
* **Pros**: Efficient, noise-tolerant.
* **Cons**: Might find only a *locally optimal* tree, not the best possible one.

---

## 🧠 5. Inductive Bias of Decision Trees

* **Bias** = preference for:

  * **Shorter trees** over longer ones.
  * Trees with **high-information-gain attributes near the root**.
* Related to **Occam’s Razor**: prefer simpler hypotheses that fit the data.
* Type of bias:

  * **Preference bias** (not restricting hypothesis space, but preferring some solutions).

---

## ⚠️ 6. Issues in Decision Tree Learning

### (a) Overfitting

* **Definition**: Hypothesis fits training data very well but performs poorly on unseen data.
* **Causes**:

  * Noise in training data.
  * Too few examples (coincidental patterns).
* **Solutions**:

  * **Pre-pruning**: stop tree growth early.
  * **Post-pruning**: grow full tree, then remove branches that don’t improve test accuracy.

### (b) Continuous Attributes

* Can be handled by splitting with thresholds (e.g., Temp > 75).

### (c) Missing Data

* Strategies: ignore example, assign most probable value, or distribute among branches.

### (d) Attribute Costs

* Some attributes may be expensive to measure → modify gain formula to account for cost.

---

## 📝 7. Key Takeaways

* Decision trees are intuitive, interpretable, and widely used.
* **ID3 algorithm** builds them using entropy + information gain.
* Hypothesis space = all finite discrete functions → very powerful.
* Bias = prefers smaller, simpler trees (Occam’s Razor).
* Main risk = **overfitting**, solved with pruning.

---
