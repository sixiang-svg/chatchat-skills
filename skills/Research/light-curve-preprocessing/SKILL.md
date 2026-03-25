---
id: light-curve-preprocessing
name: Light Curve Preprocessing
description: Systematic guidance for preprocessing astronomical light curves, including cleaning, detrending, and outlier removal.
category: Research
requires: []
examples:
  - How do I remove outliers from my TESS light curve data?
  - Guide me through detrending this light curve for planetary transit detection.
---

# Light Curve Preprocessing

Support light curve preprocessing workflows with clear steps and best practices.
## Instruction
- Load raw time-series photometry data (e.g., from TESS or Kepler) and identify systematic noise patterns.
- Implement data cleaning routines to handle missing observations and flag low-quality data points.
- Apply detrending algorithms (e.g., Gaussian Processes, Savitzky-Golay) to remove stellar variability and instrumental drifts.
- Perform sigma-clipping or specialized filtering to remove outliers without affecting legitimate transit or pulsation signals.
- Normalize the light curve to a common baseline to enable comparative analysis across multiple targets or epochs.
- Verify that the preprocessing steps haven't introduced artifacts or significantly suppressed signal depth.

## When to Use
- When preparing astronomical time-series data for exoplanet transit detection or stellar variability analysis.
- When cleaning light curve datasets from space-based telescopes (TESS, Kepler, JWST).
- When needing systematic, reproducible preprocessing for astronomical research pipelines.

## Output
- Cleaned and normalized light curve datasets in structured formats (CSV, FITS).
- Diagnostic plots showing the effects of detrending and outlier removal on the data.
- A summary of the preprocessing parameters used and the resulting data quality metrics.