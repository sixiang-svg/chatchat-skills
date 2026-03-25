---
id: pyopenms
name: pyOpenMS
description: Python bindings for OpenMS to process mass spectrometry data, including file handling, feature detection, and peptide identification.
category: Research
requires: []
examples:
  - Read an mzML file and iterate through its mass spectra.
  - Perform feature detection on mass spectrometry data using pyOpenMS.
---

# PyOpenMS

## Overview

PyOpenMS provides Python bindings to the OpenMS library for computational mass spectrometry, enabling analysis of proteomics and metabolomics data. Use for handling mass spectrometry file formats, processing spectral data, detecting features, identifying peptides/proteins, and performing quantitative analysis.

## Installation

Install using uv

Verify installation

## Core Capabilities

PyOpenMS organizes functionality into these domains:

### 1. File I/O and Data Formats

Handle mass spectrometry file formats and convert between representations.

**Supported formats**: mzML, mzXML, TraML, mzTab, FASTA, pepXML, protXML, mzIdentML, featureXML, consensusXML, idXML

Basic file reading:

### 2. Signal Processing

Process raw spectral data with smoothing, filtering, centroiding, and normalization.

Basic spectrum processing:


### 3. Feature Detection

Detect and link features across spectra and samples for quantitative analysis.

### 4. Peptide and Protein Identification

Integrate with search engines and process identification results.

**Supported engines**: Comet, Mascot, MSGFPlus, XTandem, OMSSA, Myrimatch

Basic identification workflow:

### 5. Metabolomics Analysis

Perform untargeted metabolomics preprocessing and analysis.

Typical workflow:
1. Load and process raw data
2. Detect features
3. Align retention times across samples
4. Link features to consensus map
5. Annotate with compound databases

## Data Structures

PyOpenMS uses these primary objects:

- **MSExperiment**: Collection of spectra and chromatograms
- **MSSpectrum**: Single mass spectrum with m/z and intensity pairs
- **MSChromatogram**: Chromatographic trace
- **Feature**: Detected chromatographic peak with quality metrics
- **FeatureMap**: Collection of features
- **PeptideIdentification**: Search results for peptides
- **ProteinIdentification**: Search results for proteins

## Common Workflows


### Parameter Management

Most algorithms use a parameter system

### Export to Pandas

Convert data to pandas DataFrames for analysis

## Integration with Other Tools

PyOpenMS integrates with:
- **Pandas**: Export data to DataFrames
- **NumPy**: Work with peak arrays
- **Scikit-learn**: Machine learning on MS data
- **Matplotlib/Seaborn**: Visualization
- **R**: Via rpy2 bridge

## When to Use
- When processing large-scale LC-MS/MS datasets for proteomics or metabolomics research.
- When identifying peptides and quantifying their abundance in biological samples.
- When building custom computational mass spectrometry pipelines in Python.

## Output
- Picked peaks and identified molecular features with associated intensities.
- Peptide and protein identification lists with scoring and validation metrics.
- Quantified protein expression tables ready for bioinformatics interpretation.