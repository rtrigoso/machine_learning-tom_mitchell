# 🌳 Decision Tree Learning (Chapter 3)

## 1. What is Decision Tree Learning?

* A **decision tree** is a model that classifies examples by sorting them through a tree of questions about their attributes.
* It is used for **discrete-valued target functions** (e.g., “yes/no”, or category labels).
* Strengths:

  * Works well with noisy data.
  * Can handle missing attribute values.
  * Produces human-readable rules (each path can be turned into an **if-then** rule).

🔎 **Example**: The famous **PlayTennis** dataset

* Attributes: Outlook (Sunny/Overcast/Rain), Temperature, Humidity, Wind.
* Target: PlayTennis = Yes or No.
* A decision tree can decide: *Should we play tennis today?*

### ✅ If–Then Rules (from the PlayTennis Tree)

- If Outlook = Overcast → PlayTennis = Yes
- If Outlook = Sunny ∧ Humidity = High → PlayTennis = No
- If Outlook = Sunny ∧ Humidity = Normal → PlayTennis = Yes
- If Outlook = Rain ∧ Wind = Strong → PlayTennis = No
- If Outlook = Rain ∧ Wind = Weak → PlayTennis = Yes

---

## 2. How Decision Trees Work

* Start at the **root** → test one attribute (e.g., Outlook).
* Follow the branch for the attribute value (e.g., Sunny).
* Continue testing attributes until reaching a **leaf node** → leaf = classification (Yes/No).

Each path = **conjunction** of conditions.
The whole tree = **disjunction** of these paths.

Example expression from the PlayTennis tree:

```
(Outlook = Sunny ∧ Humidity = Normal) 
∨ (Outlook = Overcast) 
∨ (Outlook = Rain ∧ Wind = Weak)
```

---

## 3. When is Decision Tree Learning Appropriate?

* Instances described by **attribute-value pairs**.
* **Discrete output values** (e.g., class labels).
* Disjunctive descriptions may be required.
* Can tolerate **errors/noise** in data.
* Can handle **missing values**.

Practical uses:

* Medical diagnosis
* Loan approval
* Equipment fault detection

---

## 4. The ID3 Algorithm (Core Idea)

Decision tree learning algorithms (like ID3, C4.5) build trees **top-down** using a greedy strategy:

1. Start with all training examples at the root.
2. Pick the attribute that best splits the data (using **information gain**).
3. Create child nodes for each attribute value.
4. Recurse until:

   * All examples at a node have the same label, OR
   * No attributes remain.

---

### 4.1 How to Pick the Best Attribute → **Information Gain**

* Based on **Entropy** (a measure of impurity in data).

  * Entropy(S) = 0 → perfectly pure (all same class).
  * Entropy(S) = 1 → maximally mixed (50/50 yes and no).
* Information Gain = reduction in entropy after splitting on an attribute.

📌 Formula:

$$
Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} Entropy(S_v)
$$

* Example: Choosing between **Humidity** and **Wind** for PlayTennis.

  * Gain(Humidity) = 0.151
  * Gain(Wind) = 0.048
    → Humidity is better (higher info gain).

---

## 5. Hypothesis Space of Decision Trees

* Decision trees can represent **any finite discrete-valued function** → very expressive.
* ID3 searches hypothesis space from **simple → complex** using info gain.
* Risks:

  * **Greedy**: no backtracking → may miss globally best tree.
  * Only keeps one hypothesis at a time (unlike Candidate-Elimination which keeps many).

---

## 6. Inductive Bias in Decision Trees

* ID3’s bias = preference for **shorter trees** + attributes with **high info gain near the root**.
* This is related to **Occam’s Razor**:
  *Prefer the simplest hypothesis that fits the data.*

---

## 7. Practical Issues

### 7.1 Overfitting

* Trees that perfectly classify training data may do **worse on unseen data**.
* Happens due to:

  * Noise in training data.
  * Coincidental patterns in small datasets.
* Solutions:

  * **Pre-pruning** → stop early before tree gets too complex.
  * **Post-pruning** → grow full tree, then prune branches that don’t help generalization.

### 7.2 Extensions

* Handle **continuous attributes** (e.g., Temperature > 75).
* Deal with **missing values**.
* Use **different attribute selection measures**.
* Consider **cost-sensitive attributes**.

---

# ✅ Summary (What You Should Take Away)

* Decision trees classify by asking attribute-based questions.
* ID3 builds trees top-down using **information gain**.
* Expressive: can represent any discrete-valued function.
* Bias: prefers smaller, simpler trees (Occam’s Razor).
* Key risk: **overfitting** → solved by pruning.
* Widely used in **classification tasks** (medical, finance, diagnostics).

---
