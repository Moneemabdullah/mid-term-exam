---
type: lecture-note
subject: Data Mining
status: supplementary
source: Scanned notebook pp. 24–25, 38–41; standard definitions
last_updated: 2026-11-23
---

# Apriori Supplement

> [!warning] Supplementary, not from the provided slides
> The provided Data Mining PDFs do not cover Apriori. This note reconstructs the topic from the cross-subject handwritten notebook (pp. 24–25, 38–41) and standard Data Mining definitions. The OCR is noisy; verify the worked example against the notebook images.

## 1. Definitions

- **Transaction:** a set of items bought together.
- **Itemset:** a set of one or more items.
- **k-itemset:** an itemset with `k` items.
- **Support count `count(X)`:** number of transactions containing itemset `X`.
- **Support `support(X)`:** fraction of all transactions containing `X`.
- **Frequent itemset:** an itemset whose support is at least the minimum support threshold.
- **Association rule:** an implication `X → Y`, where `X` and `Y` are disjoint itemsets.
  - `X` = antecedent (left-hand side)
  - `Y` = consequent (right-hand side)
- **Confidence:** how often `Y` appears when `X` appears.
- **Lift:** how much more often `X` and `Y` occur together than expected if they were independent.

## 2. Formulas

For `N` transactions:

\[
\text{support}(X) = \frac{\text{count}(X)}{N}
\]

\[
\text{support}(X \to Y) = \text{support}(X \cup Y)
\]

\[
\text{confidence}(X \to Y) = \frac{\text{support}(X \cup Y)}{\text{support}(X)}
\]

\[
\text{lift}(X \to Y) = \frac{\text{confidence}(X \to Y)}{\text{support}(Y)}
= \frac{\text{support}(X \cup Y)}{\text{support}(X)\,\text{support}(Y)}
\]

**Interpretation of lift:**

- `lift = 1`: `X` and `Y` are independent.
- `lift > 1`: positive association; `Y` is more likely when `X` occurs.
- `lift < 1`: negative association; `Y` is less likely when `X` occurs.

## 3. Apriori principle

> If an itemset is frequent, all of its subsets are frequent. If an itemset is infrequent, all of its supersets are infrequent.

This is the **downward-closure property**. It lets Apriori prune candidates without scanning the database.

## 4. Algorithm

1. Scan the database and count each 1-item candidate `C1`.
2. Keep candidates with support ≥ minimum support to form `L1`.
3. **Join:** generate candidate `k`-itemsets `Ck` from frequent `(k−1)`-itemsets `Lk−1`.
4. **Prune:** remove candidates that contain an infrequent `(k−1)`-subset.
5. Scan the database and count support for the remaining candidates.
6. Keep candidates with support ≥ minimum support to form `Lk`.
7. Repeat until no more candidates can be generated.
8. Generate association rules from the frequent itemsets and test confidence/lift.

## 5. Worked example

> [!info] Reconstructed example
> The notebook example uses Bread, Milk, and Butter. The transaction table below is reconstructed from the OCR; check the original pages 38–41 before quoting it in an exam.

| Transaction | Items |
|---|---|
| T1 | Bread, Milk, Butter |
| T2 | Bread, Butter |
| T3 | Bread, Milk |
| T4 | Milk, Butter |
| T5 | Bread, Milk, Butter |

**Minimum support = 60%.** With `N = 5`, the minimum support count is:

\[
0.60 \times 5 = 3
\]

### Step 1: 1-itemsets

| Itemset | Count | Support |
|---|---|---|
| {Bread} | 4 | 80% |
| {Milk} | 4 | 80% |
| {Butter} | 4 | 80% |

All satisfy minimum support, so `L1 = {Bread}, {Milk}, {Butter}`.

### Step 2: 2-itemsets

| Itemset | Transactions | Count | Support |
|---|---|---|---|
| {Bread, Milk} | T1, T3, T5 | 3 | 60% |
| {Bread, Butter} | T1, T2, T5 | 3 | 60% |
| {Milk, Butter} | T1, T4, T5 | 3 | 60% |

All satisfy minimum support, so all three are frequent.

### Step 3: 3-itemset

| Itemset | Transactions | Count | Support |
|---|---|---|---|
| {Bread, Milk, Butter} | T1, T5 | 2 | 40% |

40% < 60%, so `{Bread, Milk, Butter}` is **not frequent** and is pruned.

**Frequent itemsets:** `{Bread}`, `{Milk}`, `{Butter}`, `{Bread, Milk}`, `{Bread, Butter}`, `{Milk, Butter}`.

## 6. Association rules

From `{Bread, Milk}`:

- `Bread → Milk`: support = 60%, confidence = 3/4 = 75%
- `Milk → Bread`: support = 60%, confidence = 3/4 = 75%

From `{Bread, Butter}`:

- `Bread → Butter`: support = 60%, confidence = 3/4 = 75%
- `Butter → Bread`: support = 60%, confidence = 3/4 = 75%

From `{Milk, Butter}`:

- `Milk → Butter`: support = 60%, confidence = 3/4 = 75%
- `Butter → Milk`: support = 60%, confidence = 3/4 = 75%

For `Bread → Milk`:

\[
\text{lift} = \frac{0.75}{0.80} = 0.9375
\]

`lift < 1` means the association is slightly negative: Milk is slightly less likely given Bread than it is overall. The rules are still valid if the minimum confidence is 70%, but they are not positive associations by lift.

## 7. Strengths and limitations

**Strengths:**

- Simple and easy to understand.
- Uses the Apriori principle to prune the search space.
- Works well for market-basket and transactional data.

**Limitations:**

- Multiple database scans.
- Candidate generation can be expensive.
- Many candidates for dense data or low support thresholds.
- Does not handle numeric attributes directly.
- Can produce many rules; use support, confidence, and lift to filter.

## 8. Exam tips

- Always compute the minimum support count: `min_sup_count = min_sup × N`.
- Show the candidate sets `C1`, `L1`, `C2`, `L2`, `C3`, etc.
- State why a candidate is pruned.
- For each rule, show support, confidence, and lift.
- Interpret lift, not just confidence.
- If the question asks for “full math,” show the fractions and percentages.

## 9. Additional practice (generated)

> [!info] Practice only
> This is a generated practice problem, not an official question. Use it to practise a different support threshold and different item counts.

| Transaction | Items |
|---|---|
| T1 | A, B |
| T2 | A, B |
| T3 | A, C |
| T4 | B, C |
| T5 | A, B, C |

**Minimum support = 40%.** With `N = 5`, the minimum support count is `2`.

**1-itemsets:**

| Itemset | Count | Support |
|---|---|---|
| {A} | 4 | 80% |
| {B} | 4 | 80% |
| {C} | 3 | 60% |

**2-itemsets:**

| Itemset | Count | Support |
|---|---|---|
| {A, B} | 3 | 60% |
| {A, C} | 2 | 40% |
| {B, C} | 2 | 40% |

**3-itemset:** `{A, B, C}` appears only in T5, so count = 1, support = 20%. It is pruned.

**Rules:**

| Rule | Support | Confidence | Lift |
|---|---|---|---|
| A → B | 60% | 3/4 = 75% | 0.75 / 0.80 = 0.9375 |
| B → A | 60% | 3/4 = 75% | 0.75 / 0.80 = 0.9375 |
| A → C | 40% | 2/4 = 50% | 0.50 / 0.60 = 0.8333 |
| C → A | 40% | 2/3 = 66.7% | 0.667 / 0.80 = 0.8333 |
| B → C | 40% | 2/4 = 50% | 0.50 / 0.60 = 0.8333 |
| C → B | 40% | 2/3 = 66.7% | 0.667 / 0.80 = 0.8333 |

**Note:** `A → C` and `C → A` have the same support and lift but different confidence because their antecedents have different support counts.
