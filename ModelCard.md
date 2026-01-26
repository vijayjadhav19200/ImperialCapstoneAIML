# Model Card: Adaptive GP-Based Bayesian Optimisation Framework

## Model Overview

**Name:** Adaptive GP-Based Bayesian Optimisation Framework  
**Type:** Sequential decision-making framework using Gaussian Processes  
**Version:** v1.0  

This is a **decision framework rather than a single predictive model**, designed to propose optimal query points for black-box functions under uncertainty and strict evaluation constraints.

---

## Intended Use

### Suitable Applications
- Black-box optimisation with costly, delayed, or limited evaluations
- Continuous input spaces with low to moderate dimensionality
- Experimental and educational settings requiring reproducibility and transparency
- Optimisation tasks where model uncertainty must be explicitly managed

### Non-Intended Uses
- Discrete or combinatorial optimisation problems
- Settings requiring direct interpretability of the underlying objective function
- High-noise environments without repeated evaluations or noise modelling

---

## Model Details and Strategy

Across ten rounds of optimisation, the framework applies **Gaussian Process (GP) surrogate models** with either **Matérn or RBF kernels**, incorporating **Automatic Relevance Determination (ARD)** to learn input sensitivities.

### Acquisition Strategies
The optimisation strategy adapts per function and over time, using:
- Upper Confidence Bound (UCB)
- Expected Improvement (EI)
- Hybrid strategies (e.g. EI/UCB or PI/UCB)

Acquisition functions are selected based on observed performance, uncertainty estimates, and convergence behaviour.

### Candidate Generation
- **Low-dimensional functions:** dense grid-based candidate evaluation
- **Higher-dimensional functions:** constrained random sampling within valid bounds

The strategy evolves across rounds, reflecting accumulated evidence and changing uncertainty, with earlier rounds emphasising exploration and later rounds favouring exploitation and local refinement.

---

## Performance Summary

Performance is evaluated using:
- **Best observed output per function**
- **Percentage improvement relative to initial baseline**
- **Speed of convergence across rounds**

Observed improvements range from approximately **3% to over 200%**, depending on the function. Several functions achieved their strongest performance by **Week 6**, indicating effective balancing of exploration and exploitation despite the severe query constraints.

Performance assessment focuses on optimisation trajectories rather than asymptotic guarantees.

---

## Assumptions, Limitations, and Ethical Considerations

### Key Assumptions
- Objective functions are relatively smooth and stationary
- Signal-to-noise ratios are sufficient for GP modelling
- Early observations are informative enough to guide subsequent optimisation

### Limitations
- Sensitivity to kernel misspecification
- High cost of suboptimal early exploration decisions
- Limited robustness in highly multimodal or discontinuous landscapes
- Scalability constraints in higher-dimensional spaces

### Ethics and Transparency

Transparency is prioritised through:
- Explicit documentation of preprocessing steps
- Clear reporting of acquisition functions and modelling assumptions
- Preservation of raw observations alongside transformed data

This supports **reproducibility, auditability, and responsible adaptation** of the framework to real-world optimisation problems. Additional detail beyond this model card would increase complexity without materially improving clarity for the intended academic audience.

---

## Relationship to Dataset

This framework should be interpreted in conjunction with the accompanying **Datasheet**, which documents the data generation process, constraints, and intended use in detail.
