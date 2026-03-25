---
id: deeptools
name: deepTools
description: Analysis and visualization of NGS data, supporting BAM to bigWig conversion, QC plots, and TSS coverage heatmaps.
category: Research
requires: []
examples:
  - Generate a PCA plot for my ChIP-seq samples to check for correlation.
  - How do I convert my BAM files to bigWig format for visualization in IGV?
---

# deepTools

NGS analysis toolkit. BAM to bigWig conversion, QC (correlation, PCA, fingerprints), heatmaps/profiles (TSS, peaks), for ChIP-seq, RNA-seq, ATAC-seq visualization.

## Instruction
- Analyze the sequencing dataset (ChIP-seq, RNA-seq, etc.) to identify necessary QC or visualization steps.
- Guide the conversion of BAM files to bigWig format to facilitate visualization in genome browsers.
- Perform sample correlation or PCA analysis to assess biological replicate consistency.
- Create heatmaps or enrichment profiles centered on genomic features like TSS or peak regions.
- Apply appropriate normalization methods, such as RPKM or 1x coverage, to ensure inter-sample comparability.
- Recommend plotting parameters to optimize the visual clarity of sequencing signal enrichment.

## When to Use
- When visualizing the genomic distribution of NGS reads across different experimental conditions.
- When detecting sample outliers or batch effects through statistical quality control.
- When generating high-quality figures for genomic signal profiles and peak heatmaps.

## Output
- Technical steps and commands for BAM processing, normalization, and track generation.
- Interpretation of QC plots and their impact on the overall data reliability.
- Visual plans for generating publication-ready genomic enrichment figures.