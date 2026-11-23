---
type: previous-questions
subject: Data Mining
source: ClassTestQuestions.pdf
last_updated: 2026-11-23
---

# Data Mining — Previous Questions

> [!warning] No Data Mining questions found
> The provided `ClassTestQuestions.pdf` contains questions for Engineering Ethics, Artificial Intelligence, Digital Image Processing, and Sociology. It contains **no Data Mining questions**. Do not treat the items below as actual previous questions; they are teacher-suggested practice areas plus OCR’d previous-semester questions under CSE 441 / CSE 455.

## Teacher-suggested practice areas (fully solved examples)

These are high-value exam topics from the teacher suggestion and lecture material.

---

### Practice 1. Apriori — full transaction-table problem [30 marks]

**Question.** Given the transaction database below, minimum support count = 3 (60% of 5 transactions), minimum confidence = 60%.
Apply the Apriori algorithm: find frequent 1-itemsets, generate candidates at each level, prune, obtain all frequent itemsets, then generate strong association rules. Show support and confidence for each rule.

| Transaction | Items |
|---|---|
| T1 | Bread, Milk, Butter |
| T2 | Bread, Butter |
| T3 | Bread, Milk |
| T4 | Milk, Butter |
| T5 | Bread, Milk, Butter |

**Answer.**

**Marking scheme:** min-support count calc (1) + frequent 1-itemsets table (4) + frequent 2-itemsets table (4) + candidate/prune step (4) + rules table with support/confidence/lift (8) + lift interpretation (3) + final itemsets/rules (6).

**Step 0 — Minimum support count.** `N = 5`, min support = 60%, so `min_count = ceil(0.60 × 5) = 3`.

**Step 1 — Frequent 1-itemsets (L1):**

| Item | Count | Support | Frequent? (≥3) |
|---|---|---|---|
| Bread | 4 | 80% | Yes |
| Milk | 4 | 80% | Yes |
| Butter | 4 | 80% | Yes |

**Step 2 — Frequent 2-itemsets (L2):**

| Itemset | Count | Support | Frequent? (≥3) |
|---|---|---|---|
| {Bread, Milk} | 3 (T1,T3,T5) | 60% | Yes |
| {Bread, Butter} | 3 (T1,T2,T5) | 60% | Yes |
| {Milk, Butter} | 3 (T1,T4,T5) | 60% | Yes |

**Step 3 — Candidate 3-itemsets & pruning.** Join L2 → candidate `{Bread, Milk, Butter}`. Count = 2 (T1,T5), support = 40% < 60% → **pruned**. No frequent 3-itemsets; Apriori stops.

**L1 ∪ L2 (all frequent itemsets):** `{Bread}`, `{Milk}`, `{Butter}`, `{Bread, Milk}`, `{Bread, Butter}`, `{Milk, Butter}`.

**Step 4 — Strong association rules (min confidence 60%):**
Formula: `confidence(X→Y) = support(X∪Y) / support(X)` ; `lift = confidence / support(Y)`.

| Rule | Support | Confidence | Lift | Strong? (≥60%) |
|---|---|---|---|---|
| Bread → Milk | 3/5 = 60% | 3/4 = 75% | 0.75/0.80 = 0.9375 | Yes |
| Milk → Bread | 60% | 3/4 = 75% | 0.75/0.80 = 0.9375 | Yes |
| Bread → Butter | 60% | 3/4 = 75% | 0.9375 | Yes |
| Butter → Bread | 60% | 3/4 = 75% | 0.9375 | Yes |
| Milk → Butter | 60% | 3/4 = 75% | 0.9375 | Yes |
| Butter → Milk | 60% | 3/4 = 75% | 0.9375 | Yes |

**Lift interpretation:** All lifts are `0.9375 < 1`, so the rules are slightly negatively correlated / independent rather than strongly positively associated. Confidence alone (75%) looks strong, but lift corrects for the high individual support of each item.

**Lecture link:** Lecture Notes/Apriori Supplement — support, confidence, lift, Apriori principle, candidate generation/pruning.

---

### Practice 2. Data warehouse vs database + snowflake schema [30 marks]

**Question.** (a) What is a data warehouse? Distinguish it from a relational database system. [10]
(b) A data warehouse has dimensions Time, Doctor, Patient and measures Count and Charge. Draw a snowflake schema diagram. [20]

**Answer.**

**(a) Data warehouse vs relational database — marking scheme:** definition (3) + four distinguishing points with table (4) + OLTP vs OLAP (3).

A **data warehouse** is a subject-oriented, integrated, time-variant, and non-volatile collection of data that supports management decision-making (OLAP).

| Basis | Relational Database (OLTP) | Data Warehouse (OLAP) |
|---|---|---|
| Purpose | Day-to-day transactions | Analysis and decision support |
| Data | Current, detailed | Historical, summarized/aggregated |
| Users | Clerks, DBAs, applications | Analysts, managers, executives |
| Operations | Insert/update/delete (many small) | Read-heavy complex queries |
| Design | Normalized (3NF) | Denormalized / star / snowflake |
| Example | ATM withdrawal, order entry | Sales trend by quarter and doctor |

**(b) Snowflake schema — marking scheme:** fact table + measures (4) + dimension tables (6) + normalization to snowflake (6) + diagram description (4).

- **Fact table (center):** `Sales_Fact(fact_key, time_key, doctor_key, patient_key, count, charge)`
- **Dimension tables:**
  - `Time_Dim(time_key, date, day, month, quarter, year)`
  - `Doctor_Dim(doctor_key, doctor_name, dept_key, specialization)`
  - `Patient_Dim(patient_key, patient_name, age, gender, ward)`
- **Snowflake (normalize dimensions further):**
  - `Dept_Dim(dept_key, dept_name, hospital)` — linked from `Doctor_Dim`
  - `Ward_Dim(ward_key, ward_name, floor)` — linked from `Patient_Dim`

**Diagram (text):** `Sales_Fact` in the center; arrows to `Time_Dim`, `Doctor_Dim`, `Patient_Dim`; `Doctor_Dim` → `Dept_Dim`; `Patient_Dim` → `Ward_Dim`.

**Lecture link:** Chapter 1 — data warehouse vs database; star/snowflake schemas; OLAP vs OLTP.

---

### Practice 3. KDD + central tendency + dispersion + data warehouse difference [30 marks]

**Question.** (a) Why do we need data mining? Describe the steps in the KDD process. [15]
(b) What is midrange? Find mean and median for the data set: 30, 36, 47, 50, 52, 52, 60, 63, 70, 70, 110. [10]
(c) Why is a data warehouse different from a database? Justify. [5]

**Answer.**

**(a) Why data mining + KDD — marking scheme:** need (4) + seven KDD steps in order (7) + one-line purpose of each step (4).

We need data mining because manual analysis cannot find hidden, previously unknown, potentially useful patterns in large data sets.

**KDD steps:** (1) **Data cleaning** — remove noise, handle missing values. (2) **Data integration** — combine multiple sources. (3) **Data selection** — retrieve relevant data. (4) **Data transformation** — normalize/aggregate/consolidate. (5) **Data mining** — apply algorithms (classification, clustering, association). (6) **Pattern evaluation** — identify interesting patterns using measures (support, confidence, lift). (7) **Knowledge presentation** — visualization/reporting to users.

**(b) Midrange, mean, median — marking scheme:** midrange formula + value (3) + mean calculation + value (4) + median calculation + value (3).

Data set (sorted): 30, 36, 47, 50, 52, 52, 60, 63, 70, 70, 110. `n = 11`.

- **Midrange** = (min + max) / 2 = (30 + 110) / 2 = **70**.
- **Mean** = sum / n = (30+36+47+50+52+52+60+63+70+70+110) / 11 = 640 / 11 ≈ **58.18**.
- **Median:** n is odd (11), so median = value at position (n+1)/2 = 6th value = **52**.

**(c) Data warehouse vs database — marking scheme:** 3–4 justified differences (5).

A database (OLTP) supports current operations/transactions: normalized, read-write, current data, many small updates. A data warehouse (OLAP) supports historical analysis: integrated, subject-oriented, time-variant, non-volatile, denormalized/star schemas, read-heavy complex queries.

**Lecture link:** Chapter 1 — what/why data mining, KDD; Chapter 2 — central tendency, dispersion; data warehouse vs database.

---

### Practice 4. Entropy & information gain (decision tree) [20 marks]

**Question.** For the Outlook dataset, compute entropy and information gain for attribute Outlook. Show all steps. [10]
Illustrate decision-tree construction and explain how entropy/information gain guide attribute selection. [10]

**Answer.**

**Marking:** entropy formula + class probs + value (4) + gain formula + split calculation (4) + decision-tree construction steps (6) + attribute selection rationale (4).

Assume the classic Outlook play-tennis data:
- Total 14 days: 9 Play=Yes, 5 Play=No.
- Outlook: Sunny(5: 2 Yes, 3 No), Overcast(4: 4 Yes, 0 No), Rain(5: 3 Yes, 2 No).

**Entropy of S:** `p_yes = 9/14`, `p_no = 5/14`.
`H(S) = −(9/14)log2(9/14) − (5/14)log2(5/14) ≈ 0.940 bits`.

**Information gain for Outlook:**
- `H(S|Sunny) = −(2/5)log2(2/5) − (3/5)log2(3/5) ≈ 0.971`
- `H(S|Overcast) = 0` (all Yes)
- `H(S|Rain) = −(3/5)log2(3/5) − (2/5)log2(2/5) ≈ 0.971`
- Weighted avg = (5/14)(0.971) + (4/14)(0) + (5/14)(0.971) ≈ 0.693
- `Gain(S, Outlook) = 0.940 − 0.693 ≈ 0.247 bits`.

**Decision-tree construction:** Choose attribute with **highest information gain** as root (here Outlook). Split on Outlook. For each branch, if subset is pure (all Yes or all No) make a leaf; otherwise repeat on the subset with remaining attributes. Stop when pure, small, or depth limit reached. Overcast → leaf “Yes” immediately (pure), which is why Outlook is a strong root.

**Lecture link:** Lecture 2/5 — decision trees, entropy, information gain; Chapter 2 — statistics.

---

### Practice 5. Classification vs clustering + feature preprocessing [20 marks]

**Question.** Differentiate classification and clustering in goals, input data, and applications; identify the technique for spam emails and customer segmentation. [10]
Create feature vectors from customer data and demonstrate preprocessing: normalization, encoding categorical variables, handling missing values. [10]

**Answer.**

**Marking:** classification vs clustering table (6) + spam/segmentation identification (2) + feature vector (2) + encoding (2) + normalization (2) + missing values (2) + mini example (4).

| Basis | Classification | Clustering |
|---|---|---|
| Learning type | Supervised (labeled data) | Unsupervised (no labels) |
| Goal | Predict a class label | Group similar records |
| Input data | Features + known class labels | Features only |
| Output | Discrete class (spam/not spam) | Clusters (segments) |
| Example | Spam detection | Customer segmentation |

- Spam emails → **classification** (spam vs not spam).
- Customer segmentation → **clustering** (group by buying behavior).

**Preprocessing mini example.** Raw row: `Customer C1 | Age 25 | Gender Male | Purchases 3 | Spent $120`.
- **Encode categorical:** Gender → `Male = 1, Female = 0` (one-hot if many categories). Vector: `[25, 1, 3, 120]`.
- **Normalize (min-max):** `x' = (x − min)/(max − min)`. If Age ∈ [18, 60], Spent ∈ [0, 500]: Age′ = (25−18)/(60−18) = 7/42 ≈ 0.167; Spent′ = 120/500 = 0.24.
- **Handle missing values:** drop row / fill with mean/median/mode / predict. E.g., if Purchases missing, fill with mean purchases.

**Lecture link:** Lecture 2/5 — classification vs clustering; preprocessing — normalization, encoding, missing values; Chapter 2 — statistics.

---

## Previous-semester questions (scanned papers)

> [!info] Source
> Scanned CSE 4-2 previous Mid Term/Final papers from `../Previous QW/` were OCR’d. Data Mining questions appear under CSE 441 Data Mining and CSE 455 Data Warehousing/Data Mining.

### DM — Final Fall 2025, CSE 441 (page 9)

**Q1(a).** Apply Apriori to the transaction database with minimum support count 3: find frequent 1-itemsets, generate candidates at each level, prune, and obtain all frequent itemsets. [10]

**Q1(b).** From the frequent itemsets, generate strong association rules with minimum confidence 60%; show support and confidence for each rule. [10]

**Q2(a).** Construct the FP-tree for the same database with min support 3: item frequency table, sorted frequent 1-itemsets, header table, and final FP-tree with node-links. [10]

**Answer.** The OCR transaction table was not fully readable, so exact itemsets cannot be verified. Method: count each item; keep items with count ≥ 3 as frequent 1-itemsets; join frequent (k−1)-itemsets into candidates; prune candidates having any infrequent subset; scan to count candidates; repeat until no frequent k-itemset remains. For FP-tree: sort items by descending frequency, build prefix paths, compress into tree, maintain header table with node-links. For rules: `support(X→Y) = count(X∪Y)/N`; `confidence(X→Y) = support(X∪Y)/support(X)`; keep rules with confidence ≥ 60%. See `Lecture Notes/Apriori Supplement.md` for the fully worked notebook example.

**Lecture link:** Apriori Supplement; Lecture 5/9 — preprocessing and association rules.

---

### DM — Final Spring 2024, CSE 455 Data Warehousing and Data Mining (page 1)

**Q1(a).** What is a data warehouse? Distinguish it from a relational database system. [10]

**Q1(b).** A data warehouse has dimensions Time, Doctor, Patient and measures Count and Charge. Draw a snowflake schema diagram. [20]

**Answer.** See **Practice 2** above for the full, worked answer (definition, OLTP vs OLAP table, fact/dimension tables, snowflake normalization, text diagram).

**Lecture link:** Chapter 1 — data warehouse, star/snowflake schema, OLAP vs OLTP.

---

### DM — Mid Spring 2024, CSE 455 Data Warehousing and Data Mining (page 7)

**Q1(a).** Why do we need data mining? Describe the steps in the KDD process. [15]

**Q1(b).** What is midrange? Find mean and median for the given data set. [10]

**Q1(c).** Why is a data warehouse different from a database? Justify. [5]

**Answer.** See **Practice 3** above for the full, worked answer (KDD steps, midrange/mean/median with numeric example, warehouse vs database justification).

**Lecture link:** Chapter 1 — why data mining, KDD; Chapter 2 — central tendency; data warehouse vs database.

---

### DM — Final Spring 2026, CSE 441 (page 11)

**Q1(a).** For the Outlook dataset, compute entropy and information gain for attribute Outlook. Show all steps. [10]

**Q1(b).** Illustrate decision-tree construction and explain how entropy/information gain guide attribute selection. [10]

**Answer.** See **Practice 4** above for the full worked example with numbers.

**Lecture link:** Decision trees, entropy, information gain (Lecture 2/5); Chapter 2 — statistics.

---

### DM — Mid Fall 2025, CSE 441 (page 5)

**Q1(a).** Differentiate classification and clustering in goals, input data, and applications; identify the technique for spam emails and customer segmentation. [10]

**Q1(b).** Create feature vectors from customer data and demonstrate preprocessing: normalization, encoding categorical variables, handling missing values. [10]

**Answer.** See **Practice 5** above for the full worked answer with table and mini example.

**Lecture link:** Classification vs clustering; preprocessing — normalization, encoding, missing values.
