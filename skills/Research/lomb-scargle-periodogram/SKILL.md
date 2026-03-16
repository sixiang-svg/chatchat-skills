---
id: lomb-scargle-periodogram
name: Lomb Scargle Periodogram
description: Guidance for Lomb-Scargle periodogram analysis to detect periodicity in unevenly sampled astronomical time-series data.
category: Research
requires: []
examples:
  - Calculate the Lomb-Scargle periodogram for this unevenly sampled data.
  - How do I determine the false alarm probability for my periodogram peaks?
---

# Lomb Scargle Periodogram

Support lomb scargle periodogram workflows with clear steps and best practices.

## Instruction
- Identify the unevenly sampled time-series data and define the frequency range for the search.
- Execute the Lomb-Scargle algorithm to compute the power spectrum and identify significant periodic peaks.
- Determine the False Alarm Probability (FAP) to evaluate the statistical significance of identified periodogram peaks.
- Account for spectral leakage and aliasing effects that may occur due to sampling gaps or periodicities in the observing window.
- Fold the light curve on the candidate period to visually verify the phase-coherence of the signal.
- Refine the period estimation using higher-resolution frequency grids or secondary optimization methods.

## When to Use
- When detecting periodic signals (e.g., stellar rotation, orbital periods) in unevenly sampled astronomical data.
- When standard Fourier transforms are inapplicable due to gaps or irregular sampling in time-series measurements.
- When calculating the statistical significance of periodicities in scientific research datasets.

## Output
- Lomb-Scargle power spectra showing significant peaks and frequency distributions.
- Calculated period estimates with associated False Alarm Probability (FAP) scores.
- Phase-folded plots for visual verification of the identified periodic signal.