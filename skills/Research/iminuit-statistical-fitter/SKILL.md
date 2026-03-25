---
id: iminuit-statistical-fitter
name: iMinuit Statistical Fitter
description: Guidance for using iMinuit for maximum likelihood fits, least-squares estimation, and error analysis in scientific data.
category: Research
requires: []
examples:
  - Perform a maximum likelihood fit for my custom probability density function.
  - How do I calculate MINOS errors for my parameter fit using iMinuit?
---

# iMinuit Statistical Fitter

Support iminuit statistical fitter workflows with clear steps and best practices.
## Instruction
- Identify the statistical model and the corresponding loss function, such as Least Squares or Log-Likelihood.
- Define the initial parameter values and set appropriate physical limits or constraints for the fit.
- Execute the HESSE algorithm to calculate the covariance matrix and determine standard parameter errors.
- Run the MINOS algorithm for complex or non-linear models to obtain rigorous asymmetric error intervals.
- Assess the goodness-of-fit using chi-square statistics, reduced chi-square, or likelihood ratios.
- Analyze parameter correlations to identify potential model degeneracies or overfitting issues.
- Generate visualization plots showing the data points overlaid with the optimized model curve and residuals.

## When to Use
- When performing high-precision parameter estimation and error analysis on scientific experimental data.
- When custom probability density functions (PDFs) require maximum likelihood fitting.
- When rigorous error propagation and covariance matrix calculations are needed for published research.

## Output
- Optimized parameter values with associated standard or MINOS error estimates.
- A full covariance and correlation matrix for the fitted parameters.
- Statistical fit reports including Chi-square/NDF and significance levels.