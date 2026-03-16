---
id: transit-least-squares
name: Transit Least Squares
description: Step-by-step guidance for Transit Least Squares (TLS) analysis to detect periodic signals in photometric data.
category: Research
requires: []
examples:
  - Apply the Transit Least Squares algorithm to this astronomical light curve.
  - Identify periodic planet signals in my photometric data using TLS.
---

# Transit Least Squares

Support transit least squares workflows with clear steps and best practices.

## Instruction
- Load time-series photometric light curves, ensuring the data is properly cleaned and detrended.
- Define the search grid parameters, including the minimum and maximum period to be searched.
- Execute the TLS algorithm to detect periodic dips in stellar brightness, accounting for the realistic transit shape.
- Evaluate the Signal Detection Efficiency (SDE) and Signal-to-Noise Ratio (SNR) to determine the statistical significance of detected peaks.
- Identify candidate planetary transits and extract their orbital period, transit duration, and depth.
- Run a secondary optimization to refine the transit parameters and check for harmonic signals or eclipsing binary patterns.

## When to Use
- When searching for shallow planetary transit signals in light curves from missions like TESS, Kepler, or ground-based surveys.
- When traditional Box Least Squares (BLS) is insufficient for detecting signals with realistic transit profiles.
- When needing high-precision periodogram analysis for periodic signal discovery in astronomical photometry.

## Output
- TLS periodograms showing power peaks and identified period candidates.
- Summaries of planetary parameters (period, depth, duration) with associated confidence scores.
- Actionable next steps for signal validation and transit-fitting refinement.