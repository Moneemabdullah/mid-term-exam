---
type: lecture-summary
subject: Data Mining
last_updated: 2026-11-23
---

# Data Mining — Lecture Summary

> [!info] Scope
> Based on the three chapter PDFs and Lectures 2, 3, 4, 5, 5.1, and 9. Lectures 6–8 were not provided. Apriori is covered by the supplementary note because it is absent from the provided slides.

## Source map

| Source | Topics |
|---|---|
| `Study Materials/PDFs/01Intro.pdf` | What/why data mining, KDD, patterns, technologies, applications, issues |
| `Study Materials/PDFs/02Data.pdf` | Data objects, attribute types, statistics, visualization, similarity |
| `Study Materials/PDFs/03Preprocessing.pdf` | Data quality, cleaning, integration, reduction, transformation, discretization, normalization |
| `Lecture Notes/Lecture 2.pdf` | ML basics, descriptive statistics |
| `Lecture Notes/Lecture 3.pdf` | Visualization and histograms |
| `Lecture Notes/Lecture 4.pdf` | Similarity and dissimilarity |
| `Lecture Notes/Lecture 5.pdf`, `Lecture 5.1.pdf` | Data quality, preprocessing, missing values, normalization |
| `Lecture Notes/Lecture 9.pdf` | Wavelets, normalization, attribute subset selection |
| `Lecture Notes/Apriori Supplement.md` | Apriori, support, confidence, lift |

## 1. Introduction and KDD

- **Video for this topic:** [Knowledge Discovery in Database (KDD) Process](https://www.youtube.com/watch?v=L9PfNWIQ1bY) — Perfect Computer Engineer.
- **Data mining** is the process of discovering interesting, previously unknown, and potentially useful patterns from large data sets.
- It is not just extraction; it involves **knowledge discovery in databases (KDD)**.
- **KDD steps:**
  1. Data cleaning
  2. Data integration
  3. Data selection
  4. Data transformation
  5. Data mining
  6. Pattern evaluation
  7. Knowledge presentation
- **Data mining functionalities:** classification, regression, clustering, association rule mining, outlier detection, sequence mining.
- **Applications:** retail, banking, fraud detection, healthcare, telecommunications, web analytics, recommender systems.
- **Issues:** data quality, scalability, privacy, security, ethical use, noisy data, high dimensionality.

## 2. Data objects, attributes, and statistics

- **Video for attribute types:** [Scales of Measurement: Nominal, Ordinal, Interval and Ratio](https://www.youtube.com/watch?v=LuBD49SFpWs) — The Organic Chemistry Tutor.

### Attribute types

| Type | Description | Example |
|---|---|---|
| Nominal | Categories, no order | Color, gender, city |
| Binary | Two states | Yes/no, true/false |
| Ordinal | Ordered categories | Small/medium/large |
| Interval | Ordered, equal intervals, no true zero | Temperature in °C |
| Ratio | Ordered, equal intervals, true zero | Height, weight, income |

- **Discrete** attributes have finite or countable values; **continuous** attributes have real-valued values.

### Central tendency

- **Video for this topic:** [Descriptive Statistics: Mean, Median, Mode, Variance and SD](https://www.youtube.com/watch?v=SplCk-t1BeA) — Grad Coach.
- **Mean:** \(\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i\)
- **Median:** middle value after sorting; robust to outliers.
- **Mode:** most frequent value; useful for nominal data.
- **Midrange:** \((\min + \max)/2\).

### Dispersion

- **Variance:**
  \[
  \sigma^2 = \frac{1}{n}\sum_{i=1}^{n}(x_i - \bar{x})^2
  \]
- **Standard deviation:** \(\sigma = \sqrt{\sigma^2}\)
- **Range:** \(\max - \min\)
- **Quartiles:** Q1, Q2 (median), Q3; **IQR** = Q3 − Q1.

### Covariance and correlation

- **Video for this topic:** [Covariance vs Correlation](https://www.youtube.com/watch?v=sU8RsIsZ6Dg) — Unfold Data Science.
- **Covariance:**
  \[
  \text{Cov}(X,Y) = \frac{1}{n}\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})
  \]
  Positive means variables tend to move together; negative means they move in opposite directions.
- **Correlation:**
  \[
  r = \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}
  \]
  `r` is between −1 and +1. It measures the strength and direction of a linear relationship.

## 3. Similarity and dissimilarity

- **Video for this topic:** [Similarity and Dissimilarity Measures](https://www.youtube.com/watch?v=N-a1pom7J9M) — Sneha Bagalkot.
- **Similarity:** higher when objects are more alike; often in `[0,1]`.
- **Dissimilarity:** lower when objects are more alike; distance is a common example.
- **Nominal:** simple matching; count matches / total attributes.
- **Binary:** symmetric vs asymmetric; **Jaccard** for asymmetric binary data.
- **Numeric:** Minkowski distance
  \[
  d(i,j) = \left(\sum_{f=1}^{p}|x_{if} - x_{jf}|^h\right)^{1/h}
  \]
  - `h = 1`: Manhattan
  - `h = 2`: Euclidean
  - `h → ∞`: supremum/Chebyshev
- **Cosine similarity:**
  \[
  \cos(d_1,d_2) = \frac{d_1 \cdot d_2}{||d_1||\,||d_2||}
  \]
  Useful for text and high-dimensional vectors.
- **Ordinal:** replace values by ranks, map ranks to `[0,1]`, then use numeric distance.
- **Mixed types:** combine normalized distances with weights.

## 4. Data preprocessing

- **Video for missing values:** [How to Deal with Missing Values](https://www.youtube.com/watch?v=KfC7VfDfn8I) — Gate Smashers.
- **Data quality:** accuracy, completeness, consistency, timeliness, believability, interpretability.
- **Data cleaning:** handle missing values, noise, outliers, duplicates, inconsistencies.
  - Missing values: drop, fill with mean/median/mode, predict, or use a placeholder.
  - Noise: binning, regression, clustering.
- **Data integration:** combine data from multiple sources; resolve schema and entity conflicts.
- **Data reduction:** reduce volume while preserving information.
  - Dimensionality reduction: PCA, feature selection, wavelets.
  - Numerosity reduction: sampling, histograms, clustering.
- **Data transformation:** normalization, aggregation, smoothing, attribute construction.
- **Data discretization:** binning, histogram analysis, clustering, entropy-based methods.
- **Normalization:**
  - **Video for this topic:** [Normalization: Min-Max and Z-Score](https://www.youtube.com/watch?v=lggqjmQzsGI) — Gate Smashers.
  - Min-max: \(\frac{x - \min}{\max - \min}\)
  - Z-score: \(\frac{x - \mu}{\sigma}\)
  - Decimal scaling: \(\frac{x}{10^j}\)

## 5. Lectures 2–5 and 9

- **Lecture 2:** ML basics; supervised, unsupervised, semi-supervised, and reinforcement learning; classification vs regression; descriptive statistics.
- **Lecture 3:** visualization; histograms; scatter plots; box plots; data distribution.
  - **Video for visualization:** [Histograms and Box Plots](https://www.youtube.com/watch?v=AviY4MhnKTU) — Data Science Dojo.
- **Lecture 4:** similarity/dissimilarity; Euclidean, Manhattan, Jaccard, cosine.
- **Lecture 5 / 5.1:** data quality, preprocessing tasks, missing values, normalization, Python examples. The two files overlap; use one as the primary and the other as an alternate.
- **Lecture 9:** wavelet transform, data normalization (min-max, z-score, decimal scaling), attribute subset selection.
  - **Video for wavelets:** [Wavelet Transform: Concept and Solved Problem](https://www.youtube.com/watch?v=Q-_0N6CANjE) — NotesNaka.

## 6. Apriori

- **Video for this topic:** [Apriori Algorithm in Data Mining](https://www.youtube.com/watch?v=o_hnNBM0jtk) — Gate Smashers.
- Finds **frequent itemsets** and generates **association rules**.
- **Support:** fraction of transactions containing an itemset.
- **Confidence:** how often the consequent appears when the antecedent appears.
- **Lift:** whether the rule is better than random chance.
- **Apriori principle:** if an itemset is frequent, all its subsets are frequent; if an itemset is infrequent, all its supersets are infrequent.
- Full formulas and a worked example are in [[Subjects/Data Mining/Lecture Notes/Apriori Supplement|Apriori Supplement]].

## Quick formula sheet

| Measure | Formula |
|---|---|
| Mean | \(\bar{x} = \frac{1}{n}\sum x_i\) |
| Variance | \(\sigma^2 = \frac{1}{n}\sum(x_i-\bar{x})^2\) |
| Covariance | \(\text{Cov}(X,Y) = \frac{1}{n}\sum(x_i-\bar{x})(y_i-\bar{y})\) |
| Correlation | \(r = \frac{\text{Cov}(X,Y)}{\sigma_X\sigma_Y}\) |
| Min-max | \(\frac{x-\min}{\max-\min}\) |
| Z-score | \(\frac{x-\mu}{\sigma}\) |
| Support | \(\frac{\text{count}(X)}{N}\) |
| Confidence | \(\frac{\text{support}(X\cup Y)}{\text{support}(X)}\) |
| Lift | \(\frac{\text{confidence}(X\to Y)}{\text{support}(Y)}\) |

## Gaps

- Official syllabus not provided.
- Lectures 6, 7, and 8 not provided.
- Apriori is not in the provided slides; the supplement is based on the notebook and standard definitions.
- No Data Mining previous questions were provided.
