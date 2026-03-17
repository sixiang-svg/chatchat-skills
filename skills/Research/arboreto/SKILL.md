---
id: arboreto
name: Arboreto
description: Infer gene regulatory networks from expression data using GRNBoost2 and GENIE3 algorithms.
category: research
requires: []
examples:
  - Infer a gene regulatory network from this expression matrix using GRNBoost2.
  - How do I set up a distributed Dask client for Arboreto?
---
# Gene Regulatory Network (GRN) Inference Instructions

## Purpose
Guide the agent in assisting users with the inference of gene regulatory networks from expression data using the Arboreto library. This includes algorithm selection, environment setup, and results interpretation.

## Instructions
1. **Data Preparation**: Instruct the user to format their gene expression data as a matrix where genes are columns and observations (cells or samples) are rows. Verify if a specific list of Transcription Factors (TFs) is available to refine the search.
2. **Algorithm Selection Strategy**:
    - **GRNBoost2**: Recommend this as the default for large-scale datasets (10k+ observations) due to its superior speed and gradient boosting optimization.
    - **GENIE3**: Suggest this for smaller datasets or when validation against classic Random Forest-based methods is required.
3. **Execution Logic**:
    - Advise the user to always wrap execution logic within an `if __name__ == '__main__':` guard to prevent process spawning errors in Dask.
    - Explain the use of a random `seed` to ensure reproducibility across different runs.
4. **Computational Scaling**:
    - For local use, explain that Arboreto automatically utilizes all available cores.
    - For high-performance computing, guide the user on configuring a `LocalCluster` with specific memory limits or connecting to a remote Dask scheduler using a TCP address.

## Output
When providing results or guiding the user on data export, ensure the following structure:
- **Columns**: The output must contain three mandatory columns: `TF` (Regulator), `target` (Target Gene), and `importance` (Regulatory Score).
- **Ranking**: Sort results by the `importance` score in descending order.
- **Filtering Advice**: Suggest the user filter high-confidence links using a threshold (e.g., importance > 0.5) or by selecting the top N links per target gene.

## Implementation Constraints
- **Self-Contained Setup**: Do not provide raw bash scripts for installation. Instead, advise the user on necessary dependencies like `scipy`, `scikit-learn`, `pandas`, and `dask`.
- **Troubleshooting Guidance**: If the user encounters memory errors, proactively suggest filtering low-variance genes or increasing Dask worker resources.
- **Clarity**: Ensure that the distinction between "Regulators" and "Targets" is maintained throughout the analysis process.

## Best Practices
- Encourage the use of multiple seeds to identify consensus links for greater biological robustness.
- Mention integration with downstream pipelines like pySCENIC for further regulon activity scoring.