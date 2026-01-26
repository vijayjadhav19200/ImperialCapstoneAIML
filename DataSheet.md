# Datasheet for BBO Capstone Optimisation Dataset

## Overview and Motivation

This dataset was created as part of a capstone project applying **Bayesian Optimisation (BO)** to maximise the outputs of a set of unknown (black-box) functions under realistic operational constraints. Each function represents a simulated real-world optimisation problem where the internal structure is hidden and only input–output observations are available.

A key constraint of the project is that **only one query per function can be submitted per week**, with **delayed feedback**, forcing careful trade-offs between exploration and exploitation. This setup mirrors real-world optimisation scenarios such as experimental design, engineering tuning, and policy optimisation, where evaluations are costly, slow, or opaque.

The dataset and modelling framework were created by **Vijay Jadhav** as part of an academic capstone project, with no external funding. The primary motivation is to study **sequential decision-making under uncertainty** and to analyse how modelling assumptions, acquisition strategies, and early decisions influence downstream optimisation performance.

---

## Dataset Composition and Collection

### Dataset Structure

The dataset consists of **eight independent black-box optimisation problems**, each corresponding to a different hidden objective function. Input dimensionality varies across functions, ranging from **1D to 8D**.

Each data instance represents:
- A weekly query (input vector)
- The corresponding observed scalar output returned by the black-box function

Data is collected incrementally over **ten weekly rounds**, resulting in:
- 10 observations per function
- 80 total function evaluations across the dataset

All data is numerical and synthetic. There is no personal, sensitive, or offensive content.

### Collection Process

Queries are generated using a **deterministic, adaptive sampling strategy** driven by Bayesian Optimisation. At each round, a surrogate model is fit using all previously observed data for a given function, and a new query is selected by maximising an acquisition function.

There are:
- No missing values
- No fixed train/test splits  
Models are retrained each week using the full observation history available at that time.

The dataset is **complete relative to the allowed evaluation budget**, but it is not exhaustive with respect to the underlying function domains due to strict query limits.

---

## Preprocessing and Data Handling

Preprocessing is applied on a per-function basis and includes:

- **Input scaling and standardisation**
- **Output transformations**, such as:
  - Log transforms
  - Signed root transforms
  - Yeo–Johnson transformations
- **Outlier handling**, where required, using techniques such as One-Class SVM
- **Automatic Relevance Determination (ARD)** to infer input importance

To support transparency and reproducibility:
- Raw observations are preserved
- Transformed versions are stored or reproducible via documented preprocessing steps

No data is removed; transformations are applied solely to improve model stability and optimisation performance.

---

## Intended Uses and Limitations (Dataset)

### Intended Uses
- Educational and experimental study of Bayesian Optimisation
- Analysis of exploration–exploitation trade-offs under tight evaluation budgets
- Investigation of sensitivity to early observations and modelling assumptions
- Benchmarking adaptive optimisation strategies in low-data regimes

### Limitations and Non-Intended Uses
- The dataset is **not suitable for fairness analysis**
- Not designed for real-time decision systems
- Not appropriate for direct deployment in high-stakes domains without domain-specific validation
- Results are sensitive to kernel choice, preprocessing decisions, and early sampling outcomes

---

## Distribution and Maintenance

- The dataset is stored and maintained as part of the capstone project repository
- Intended for academic and educational use
- Redistribution is subject to course and institutional guidelines
- The dataset is frozen after completion of the ten optimisation rounds to preserve reproducibility
