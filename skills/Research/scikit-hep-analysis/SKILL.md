---
id: scikit-hep-analysis
name: Scikit-HEP Analysis
description: Step-by-step guidance for high-energy physics analysis workflows using the Scikit-HEP library.
category: Research
requires: []
examples:
  - Help me set up a Scikit-HEP workflow for my particle physics data.
  - What are the best practices for using Scikit-HEP in data analysis?
---

# Scikit-HEP Analysis

Support scikit-hep workflows with clear steps and best practices.

## Instruction
- Utilize the Scikit-HEP ecosystem tools, specifically `uproot` and `awkward-array`, to access and manipulate large-scale physics datasets in ROOT format.
- Perform high-performance data processing on jagged (non-rectilinear) arrays commonly found in particle collision events.
- Implement histogramming and visualization using `boost-histogram` or `mplhep` to generate publication-quality physics plots.
- Execute statistical fitting and parameter estimation tasks using wrappers for `iminuit` or `zfit`.
- Conduct decay chain analysis and kinematic calculations for particle identification and event reconstruction.
- Follow best practices for memory management when processing multi-terabyte HEP datasets on distributed systems.

## When to Use
- When performing data analysis for high-energy physics experiments (e.g., LHC, Belle II) using the Python scientific stack.
- When needing to read or write ROOT files without a full ROOT installation.
- When visualizing and fitting complex particle physics histograms and distributions.

## Output
- Summarized HEP analysis plans including data loading strategies and selection cuts.
- Annotated physics plots (e.g., invariant mass distributions) with statistical fit results.
- Performance-optimized Python code snippets for HEP data manipulation.
