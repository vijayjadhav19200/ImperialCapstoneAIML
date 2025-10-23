# Project Overview

This capstone project simulates a Bayesian optimisation-style competition, where the objective is to find the maximum value of eight unknown black-box functions.
Each function represents a real-world problem such as radiation detection, drug discovery, process optimisation, or hyperparameter tuning — scenarios where evaluations are costly, noisy, or limited.

Unlike traditional optimisation, where the mathematical form of a function is known, here the function equations and landscapes are hidden. You can only observe outputs from selected input queries. This setup mirrors real-world machine learning challenges, where systems often operate with incomplete information and must learn intelligently from limited data.

### The high-level goal is to:

- Use intelligent search strategies to maximise outputs for each unknown function.
- Develop adaptive models that can balance exploration (searching new areas) and exploitation (refining promising regions).
- Demonstrate strong reasoning under uncertainty — a key skill for any data scientist or ML engineer.

### This project supports my future career by strengthening skills in:

- Experimental design and adaptive learning
- Model-based optimisation
- Data-driven decision-making in resource-limited settings
- Applying Bayesian reasoning to real-world ML systems

# Inputs and Outputs

Each function accepts numerical inputs (arrays of varying dimensionality) and returns a scalar output representing performance or score.

| Function       | Input Format    | Output Format  | Optimisation Goal | Description                                                                                                        |
| -------------- | --------------- | -------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Function 1** | 2D array (10,2) | 1D array (10,) | Maximise          | Simulates radiation field detection. The goal is to tune detection parameters to identify strong and weak sources. |
| **Function 2** | 2D array (10,2) | 1D array (10,) | Maximise          | Models a noisy ML objective. The task is to maximise a log-likelihood-like response using Bayesian optimisation.   |
| **Function 3** | 3D array (15,3) | 1D array (15,) | Maximise          | Drug discovery task with three compound concentrations; output represents adverse effects or transformed scores.   |
| **Function 4** | 4D array (30,4) | 1D array (30,) | Maximise          | Product placement optimisation problem — tune four hyperparameters to approximate an expensive baseline model.     |
| **Function 5** | 4D array (20,4) | 1D array (20,) | Maximise          | Chemical yield optimisation task with a unimodal response surface.                                                 |
| **Function 6** | 5D array (20,5) | 1D array (20,) | Maximise          | Recipe optimisation problem — each input ingredient affects overall quality score.                                 |
| **Function 7** | 6D array (30,6) | 1D array (30,) | Maximise          | Hyperparameter tuning for an ML model with six tunable parameters.                                                 |
| **Function 8** | 8D array (40,8) | 1D array (40,) | Maximise          | High-dimensional function representing complex system optimisation, such as model architecture search.             |

Each week, we will:
- Review existing data that grows week by week
- Choose a new input point (x) to query per function
- Submit the chosen input via the capstone project portal in the required format
- Receive the new output (y) once the submission is processed
- Update the data set and revise the strategy

# Challenge Objectives

The primary goal of the BBO challenge is to maximise each function’s output using as few evaluations as possible.

Key constraints and considerations:

- Black-box functions: Internal structure and gradients are unknown.
- Limited evaluations: Each query (function evaluation) is expensive.
- Noisy responses: Output values may contain randomness or measurement noise.
- Dimensionality increases: From 2D (Function 1) up to 8D (Function 8), increasing complexity.

The challenge tests the ability to:
- Design efficient surrogate models that approximate unknown functions.
- Use acquisition functions (e.g., Expected Improvement, Upper Confidence Bound) to guide sampling.
- Balance exploration (learning the function shape) with exploitation (refining promising regions).

# Technical Approach

This section describes my evolving strategy across the early stages of the project.

#### Initial Phase (Rounds 1–3): Foundational Exploration
- Begain by fitting Gaussian Process Regression (GPR) models to the initial datasets.
- Use Expected Improvement (EI) and Upper Confidence Bound (UCB) acquisition functions.
  - EI focused on exploitation for functions with clear performance trends (Functions 2–5, 7, 8).
  - UCB encouraged exploration for uncertain or noisy functions (Functions 1 and 6).
- Normalise input ranges and outputs for stability.

#### Modeling Approach
- Construct surrogate models to estimate the mean and variance of unknown functions.
- Use the model to suggest new query points where improvement was most probable.
- For higher-dimensional functions, experiment with:
  - Random restarts of acquisition optimisation.
  - Dimensionality-aware kernel tuning.

#### Exploration vs. Exploitation
- Adjust acquisition hyperparameters dynamically:
  - Higher exploration coefficient early in optimisation.
  - Gradual shift towards exploitation as model confidence improves.
- Consider spatial diversity of query points to avoid local maxima.

#### Future Directions
- Incorporate SVM classifiers to separate high vs low-performance regions and focus search around decision boundaries.
- Test Bayesian Neural Networks (BNNs) for better scalability in higher dimensions.
- Implement batch Bayesian optimisation to suggest multiple queries simultaneously.
- Evaluate model performance through convergence metrics and visualisation of sampled points.

