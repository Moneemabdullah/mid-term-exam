---
type: previous-questions
subject: Data Mining
source: ClassTestQuestions.pdf
last_updated: 2026-11-23
---

# Data Mining — Previous Questions

> [!warning] No Data Mining questions found
> The provided `ClassTestQuestions.pdf` contains questions for Engineering Ethics, Artificial Intelligence, Digital Image Processing, and Sociology. It contains **no Data Mining questions**. Do not treat the items below as actual previous questions.

## Actual previous questions

- None found in the provided class-test paper.

## Teacher-suggested practice areas

These are topics, not transcribed questions. Use them to build practice problems from the lecture material.

| Area | Suggested practice | Source |
|---|---|---|
| Apriori | Two full transaction-table problems: frequent itemsets, support, confidence, lift, candidate generation, pruning | Teacher suggestion |
| Apriori theory | Definition, Apriori principle, algorithm steps, strengths, limitations | Teacher suggestion |
| Central tendency | Compute mean, median, and mode for a small data set; interpret each | Teacher suggestion |
| Dispersion | Compute variance and standard deviation; explain what they measure | Chapter 2 |
| Covariance and correlation | Compute covariance and correlation; interpret sign and strength | Chapter 2; teacher suggestion |
| Similarity | Compute Euclidean, Manhattan, Minkowski, Jaccard, and cosine similarity | Chapter 2; Lecture 4 |
| Intro theory | Define data mining, explain KDD, list applications and issues | Chapter 1; teacher suggestion |

## Practice status

- [ ] Solve one full Apriori problem without notes.
- [ ] Solve a second Apriori problem with different support/confidence thresholds.
- [ ] Compute mean, median, mode, variance, covariance, and correlation for one data set.
- [ ] Compute Euclidean, Manhattan, Jaccard, and cosine similarity for one example.
- [ ] Write a short KDD answer.

## Related notes

- [Apriori Supplement](Lecture Notes/Apriori Supplement.md)
- [Lecture Summary](Lecture Summary.md)
- [Important Topics](Important Topics.md)

## Previous-semester questions (scanned papers)

> [!info] Source
> Scanned CSE 4-2 previous Mid Term/Final papers from `../Previous QW/` were OCR’d. Data Mining questions appear under CSE 441 Data Mining and CSE 455 Data Warehousing/Data Mining. Some tables are OCR-garbled; where a numeric table cannot be read, the method/formula is given.

### DM — Final Fall 2025, CSE 441 (page 9)
**Q1(a).** Apply Apriori to the transaction database with minimum support count 3: find frequent 1-itemsets, generate candidates at each level, prune, and obtain all frequent itemsets. [10]
**Q1(b).** From the frequent itemsets, generate strong association rules with minimum confidence 60%; show support and confidence for each rule. [10]
**Q2(a).** Construct the FP-tree for the same database with min support 3: item frequency table, sorted frequent 1-itemsets, header table, and final FP-tree with node-links. [10]

**Answer.**
The OCR transaction table is not fully readable, so exact itemsets cannot be verified. Method: count each item; keep items with count ≥ 3 as frequent 1-itemsets; join frequent (k−1)-itemsets into candidates; prune candidates with any infrequent subset; scan to count candidates; repeat until no frequent k-itemset remains. For a rule X → Y: support = count(X∪Y)/N, confidence = support(X∪Y)/support(X), lift = confidence/support(Y). Keep rules with confidence ≥ 60%. See `Lecture Notes/Apriori Supplement.md` for the fully worked notebook example.

### DM — Final Spring 2024, CSE 455 Data Warehousing and Data Mining (page 1)
**Q1(a).** What is a data warehouse? Distinguish it from a relational database system. [10]
**Q1(b).** A data warehouse has dimensions time, doctor, patient and measures count and charge. Draw a snowflake schema diagram. [20]

**Answer.**
(a) A **data warehouse** is a subject-oriented, integrated, time-variant, non-volatile collection of data supporting management decisions. Unlike relational databases (OLTP), which are optimized for current transactions, normalization, and many small updates, a data warehouse (OLAP) is optimized for analysis: denormalized/star schemas, historical data, aggregations, and complex queries.
(b) Snowflake schema: central **fact table** (count, charge, foreign keys to dimensions). Dimension tables: **Time** (date, day, month, quarter, year), **Doctor** (doctor_id, name, dept, specialization), **Patient** (patient_id, name, age, gender, ward). Normalize dimension tables further (e.g., Doctor → Department table) to form snowflakes; draw the fact table in the center with arrows to normalized dimension tables.

### DM — Mid Spring 2024, CSE 455 Data Warehousing and Data Mining (page 7)
**Q1(a).** Why do we need data mining? Describe the steps in the KDD process. [15]
**Q1(b).** What is midrange? Find mean and median for the given data set. [10]
**Q1(c).** Why is a data warehouse different from a database? Justify. [5]

**Answer.**
(a) Data mining is needed to find useful patterns in large data that manual analysis cannot handle. **KDD steps:** data cleaning → integration → selection → transformation → data mining → pattern evaluation → knowledge presentation.
(b) **Midrange** = (min + max) / 2. The data-set table was OCR-garbled, so exact mean/median cannot be computed; for a sorted list of n values, median is the middle value (or average of the two middle values if n is even), and mean = sum/n.
(c) A database supports current operations/transactions (OLTP), while a data warehouse supports historical analysis and decisions (OLAP): integrated, subject-oriented, time-variant, non-volatile, and read-heavy.

### DM — Final Spring 2026, CSE 441 (page 11)
**Q1(a).** For the Outlook dataset, compute entropy and information gain for attribute Outlook. Show all steps. [10]
**Q1(b).** Illustrate decision-tree construction and explain how entropy/information gain guide attribute selection. [10]

**Answer.**
The Outlook table was OCR-garbled, so exact counts cannot be verified. Method: entropy(S) = -Σ p_i log2 p_i over classes. For Outlook values v ∈ {Sunny, Overcast, Rain}, Gain(S, Outlook) = entropy(S) − Σ (|S_v|/|S|) entropy(S_v). Choose the attribute with highest gain as the root, split, and repeat recursively on subsets; stop when pure, small, or depth limit is reached.

### DM — Mid Fall 2025, CSE 441 (page 5)
**Q1(a).** Differentiate classification and clustering in goals, input data, and applications; identify the technique for spam emails and customer segmentation. [10]
**Q1(b).** Create feature vectors from customer data and demonstrate preprocessing: normalization, encoding categorical variables, handling missing values. [10]

**Answer.**
(a) **Classification:** supervised; input has labeled examples; goal is to predict a class label. Example: spam detection (spam/not spam). **Clustering:** unsupervised; input has no labels; goal is to group similar records. Example: customer segmentation by buying behavior. Use classification for spam; clustering for segmentation.
(b) Create one row per customer with features: age, gender, browsing history, categories, discounts, past purchases. Encode categorical variables (one-hot/ordinal), normalize numeric features (min-max or z-score), and handle missing values by dropping, mean/median/mode imputation, or prediction. Show one mini example row and transformed numeric vector.
