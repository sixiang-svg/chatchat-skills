---
id: scanpy
name: Scanpy
description: Query CZ CELLxGENE Census (61M+ cells) for single-cell genomics data filtered by cell type, tissue, or disease.
category: Research
requires: []
examples:
  - Retrieve human macrophage expression data from the CELLxGENE Census.
  - Filter for cells with a specific disease state in the CZ CELLxGENE database.
---

# CZ CELLxGENE Census

## Overview

The CZ CELLxGENE Census provides programmatic access to a comprehensive, versioned collection of standardized single-cell genomics data from CZ CELLxGENE Discover. This skill enables efficient querying and analysis of millions of cells across thousands of datasets.

The Census includes:
- **61+ million cells** from human and mouse
- **Standardized metadata** (cell types, tissues, diseases, donors)
- **Raw gene expression** matrices
- **Pre-calculated embeddings** and statistics
- **Integration with PyTorch, scanpy, and other analysis tools**

## When to Use This Skill

This skill should be used when:
- Querying single-cell expression data by cell type, tissue, or disease
- Exploring available single-cell datasets and metadata
- Training machine learning models on single-cell data
- Performing large-scale cross-dataset analyses
- Integrating Census data with scanpy or other analysis frameworks
- Computing statistics across millions of cells
- Accessing pre-calculated embeddings or model predictions

## Instruction
- Initialize the CELLxGENE Census connection by selecting the appropriate SOMA environment for large-scale data access.
- Formulate metadata filters using `obs_value_filter` to target specific cell types, tissues, or disease states (e.g., "is_primary_data == True").
- Retrieve high-dimensional gene expression matrices and convert them into AnnData objects for integration with scanpy analysis.
- Implement out-of-core processing or batch loading for queries returning millions of cells to prevent memory errors.
- Conduct cross-tissue or cross-disease analysis by aggregating standardized data from multiple studies within the Census.
- Utilize pre-calculated embeddings and statistics from the Census to accelerate cell clustering and visualization tasks.

## Output
- Filtered AnnData objects ready for downstream scanpy analysis and clustering.
- Summaries of retrieved datasets including cell counts, tissue distribution, and metadata coverage.
- Step-by-step guidance for efficient data querying and memory management during large-scale retrieval.

## Installation and Setup

Install the Census API:

For machine learning workflows, install additional dependencies:


## Core Workflow Patterns

### 1. Opening the Census

Always use the context manager to ensure proper resource cleanup:

### 2. Exploring Census Information

Before querying expression data, explore available datasets and metadata.

### 3. Querying Expression Data (Small to Medium Scale)

For queries returning < 100k cells that fit in memory, use `get_anndata()`:


### 4. Large-Scale Queries (Out-of-Core Processing)

For queries exceeding available RAM, use `axis_query()` with iterative processing:


### 5. Machine Learning with PyTorch

For training models, use the experimental PyTorch integration:


### 6. Integration with Scanpy

Seamlessly integrate Census data with scanpy workflows:

### 7. Multi-Dataset Integration

Query and integrate multiple datasets:


## Key Concepts and Best Practices

### Always Filter for Primary Data
Unless analyzing duplicates, always include `is_primary_data == True` in queries to avoid counting cells multiple times:

### Specify Census Version for Reproducibility
Always specify the Census version in production analyses:


### Estimate Query Size Before Loading
For large queries, first check the number of cells to avoid memory issues:


### Use tissue_general for Broader Groupings

### Select Only Needed Columns
Minimize data transfer by specifying only required metadata columns

### Check Dataset Presence for Gene-Specific Queries
When analyzing specific genes, verify which datasets measured them


### Two-Step Workflow: Explore Then Query
First explore metadata to understand available data, then query expression:

# Step 1: Explore what's available
metadata = cellxgene_census.get_obs(
    census, "homo_sapiens",
    value_filter="disease == 'COVID-19' and is_primary_data == True",
    column_names=["cell_type", "tissue_general"]
)
print(metadata.value_counts())

# Step 2: Query based on findings
adata = cellxgene_census.get_anndata(
    census=census,
    organism="Homo sapiens",
    obs_value_filter="disease == 'COVID-19' and cell_type == 'T cell' and is_primary_data == True",
)

## Reference Documentation

This skill includes detailed reference documentation:

### references/census_schema.md
Comprehensive documentation of:
- Census data structure and organization
- All available metadata fields
- Value filter syntax and operators
- SOMA object types
- Data inclusion criteria

**When to read:** When you need detailed schema information, full list of metadata fields, or complex filter syntax.

### references/common_patterns.md
Examples and patterns for:
- Exploratory queries (metadata only)
- Small-to-medium queries (AnnData)
- Large queries (out-of-core processing)
- PyTorch integration
- Scanpy integration workflows
- Multi-dataset integration
- Best practices and common pitfalls

**When to read:** When implementing specific query patterns, looking for code examples, or troubleshooting common issues.

## Common Use Cases

### Use Case 1: Explore Cell Types in a Tissue

### Use Case 2: Train Cell Type Classifier

### Use Case 3: Cross-Tissue Analysis

## Troubleshooting

### Query Returns Too Many Cells
- Add more specific filters to reduce scope
- Use `tissue` instead of `tissue_general` for finer granularity
- Filter by specific `dataset_id` if known
- Switch to out-of-core processing for large queries

### Memory Errors
- Reduce query scope with more restrictive filters
- Select fewer genes with `var_value_filter`
- Use out-of-core processing with `axis_query()`
- Process data in batches

### Duplicate Cells in Results
- Always include `is_primary_data == True` in filters
- Check if intentionally querying across multiple datasets

### Gene Not Found
- Verify gene name spelling (case-sensitive)
- Try Ensembl ID with `feature_id` instead of `feature_name`
- Check dataset presence matrix to see if gene was measured
- Some genes may have been filtered during Census construction

### Version Inconsistencies
- Always specify `census_version` explicitly
- Use same version across all analyses
- Check release notes for version-specific changes
