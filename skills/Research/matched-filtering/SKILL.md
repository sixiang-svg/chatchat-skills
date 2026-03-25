---
id: matched-filtering
name: Matched Filtering
description: Step-by-step guidance and best practices for implementing matched filtering in signal processing.
category: Research
requires: []
examples:
  - How do I implement matched filtering for signal detection in noise?
  - Provide a step-by-step guide for designing a matched filter for my dataset.
---

# Matched Filtering

Support matched filtering workflows with clear steps and best practices.

## Instruction
- Define the reference template or "golden" signal that represents the expected waveform to be detected.
- Normalize both the input data stream and the template signal to ensure consistent amplitude scaling.
- Perform a cross-correlation between the input signal and the time-reversed template to maximize the signal-to-noise ratio (SNR).
- Apply a thresholding mechanism to identify peaks in the filter output that correspond to valid signal detections.
- Handle edge effects and computational overhead by utilizing FFT-based convolution for large datasets.
- Evaluate the detection performance using ROC curves or probability of detection vs. false alarm rate.

## When to Use
- When needing to extract a known signal pattern from a high-noise environment.
- When performing radar, sonar, or digital communication synchronization tasks.
- When identifying specific waveform transients in seismic, acoustic, or biomedical time-series data.

## Output
- A summarized signal detection plan including template parameters and threshold settings.
- Processed time-series data showing the filtered output and identified detection peaks.
- Performance metrics such as SNR improvement and detection confidence levels.