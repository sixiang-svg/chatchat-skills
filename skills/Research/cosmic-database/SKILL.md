---
id: cosmic-database
name: Cosmic Database
description: Access COSMIC cancer mutation database for somatic mutations, Cancer Gene Census, and mutational signature research.
category: Research
requires: []
examples:
  - Download the Cancer Gene Census from the COSMIC database.
  - Retrieve mutational signature profiles for SBS signatures.
---

# COSMIC Database

## Overview

COSMIC (Catalogue of Somatic Mutations in Cancer) is the world's largest and most comprehensive database for exploring somatic mutations in human cancer. Access COSMIC's extensive collection of cancer genomics data, including millions of mutations across thousands of cancer types, curated gene lists, mutational signatures, and clinical annotations programmatically.

## When to Use This Skill

This skill should be used when:
- Downloading cancer mutation data from COSMIC
- Accessing the Cancer Gene Census for curated cancer gene lists
- Retrieving mutational signature profiles
- Querying structural variants, copy number alterations, or gene fusions
- Analyzing drug resistance mutations
- Working with cancer cell line genomics data
- Integrating cancer mutation data into bioinformatics pipelines
- Researching specific genes or mutations in cancer contexts

## Instruction
You are a Cancer Genomics Data Scientist. When this skill is activated, you must guide the user through accessing and analyzing the COSMIC (Catalogue of Somatic Mutations in Cancer) database using the following behavioral logic:

1. **Data Acquisition Strategy**: 
    - Guide the user in downloading core datasets: **Mutations** (TSV or VCF), **Cancer Gene Census (CGC)**, and **Mutational Signatures**.
    - Explain the logic of genome assembly selection (GRCh38 vs. GRCh37) and versioning (e.g., using "latest" vs. specific versions for reproducibility).
2. **Cancer Gene Census (CGC) Analysis**: 
    - Instruct the user on identifying curated cancer genes and their specific roles (e.g., Oncogene vs. Tumor Suppressor).
    - Describe the logic for filtering experimental results based on these high-confidence gene lists.
3. **Mutation & Signature Profiles**: 
    - Guide the retrieval of SBS (Single Base Substitution), DBS (Doublet), and ID (Indel) signatures for mutational signature analysis.
    - Explain the process of extracting somatic mutation data for specific cancer types or primary sites.
4. **Large-Scale Data Integration**: 
    - Describe the logic for parsing large TSV/VCF files efficiently using tools like Pandas or Pysam.
    - Guide the integration of COSMIC data with downstream variant annotation tools (e.g., VEP, ANNOVAR).
5. **Compliance & Licensing Awareness**: Ensure the logic accounts for account registration and commercial vs. academic licensing requirements.


## Output
Your response must be structured to provide a professional cancer genomics roadmap:

### 1. Data Retrieval & Source Strategy
- **Data Selection**: Summary of the files to be downloaded (e.g., "CGC CSV" and "Mutant Export TSV") based on the research goal.
- **Assembly Confirmation**: Verification of the coordinate system (GRCh38/37) to ensure downstream compatibility.

### 2. Implementation Logic (Natural Language)
- **Download & Authentication Flow**: Step-by-step guidance on the API/script-based download process using credentials.
- **Analytical Filtering**: Natural language description of how to filter and analyze the data (e.g., "Extracting TP53 mutations from lung cancer samples").

### 3. Best Practices & Troubleshooting
- **Memory & Storage Warnings**: Advice on handling multi-GB datasets and ensuring sufficient disk space.
- **Integration Tips**: Logic for mapping COSMIC data to other cancer platforms like cBioPortal or OncoKB.

## Available Data Types

### Core Mutations
Download comprehensive mutation data including point mutations, indels, and genomic annotations.

**Common data types**:
- `mutations` - Complete coding mutations (TSV format)
- `mutations_vcf` - Coding mutations in VCF format
- `sample_info` - Sample metadata and tumor information


### Cancer Gene Census
Access the expert-curated list of ~700+ cancer genes with substantial evidence of cancer involvement.


**Use cases**:
- Identifying known cancer genes
- Filtering variants by cancer relevance
- Understanding gene roles (oncogene vs tumor suppressor)
- Target gene selection for research

### Mutational Signatures
Download signature profiles for mutational signature analysis.

**Signature types**:
- Single Base Substitution (SBS) signatures
- Doublet Base Substitution (DBS) signatures
- Insertion/Deletion (ID) signatures

### Structural Variants and Fusions
Access gene fusion data and structural rearrangements.


### Copy Number and Expression
Retrieve copy number alterations and gene expression data.


### Resistance Mutations
Access drug resistance mutation data with clinical annotations.


## Working with COSMIC Data

### Genome Assemblies
COSMIC provides data for two reference genomes:
- **GRCh38** (recommended, current standard)
- **GRCh37** (legacy, for older pipelines)


### Versioning
- Use `latest` in file paths to always get the most recent release
- COSMIC is updated quarterly (current version: v102, May 2025)
- Specific versions can be used for reproducibility: `v102`, `v101`, etc.

### File Formats
- **TSV/CSV**: Tab/comma-separated, gzip compressed, read with pandas
- **VCF**: Standard variant format, use with pysam, bcftools, or GATK
- All files include headers describing column contents


## Data Reference

For comprehensive information about COSMIC data structure, available files, and field descriptions, see `references/cosmic_data_reference.md`. This reference includes:

- Complete list of available data types and files
- Detailed field descriptions for each file type
- File format specifications
- Common file paths and naming conventions
- Data update schedule and versioning
- Citation information

Use this reference when:
- Exploring what data is available in COSMIC
- Understanding specific field meanings
- Determining the correct file path for a data type
- Planning analysis workflows with COSMIC data

## Helper Functions

The download script includes helper functions for common operations:

### Get Common File Paths

**Available shortcuts**:
- `mutations` - Core coding mutations
- `mutations_vcf` - VCF format mutations
- `gene_census` - Cancer Gene Census
- `resistance_mutations` - Drug resistance data
- `structural_variants` - Structural variants
- `gene_expression` - Expression data
- `copy_number` - Copy number alterations
- `fusion_genes` - Gene fusions
- `signatures` - Mutational signatures
- `sample_info` - Sample metadata

## Troubleshooting

### Authentication Errors
- Verify email and password are correct
- Ensure account is registered at cancer.sanger.ac.uk/cosmic
- Check if commercial license is required for your use case

### File Not Found
- Verify the filepath is correct
- Check that the requested version exists
- Use `latest` for the most recent version
- Confirm genome assembly (GRCh37 vs GRCh38) is correct

### Large File Downloads
- COSMIC files can be several GB in size
- Ensure sufficient disk space
- Download may take several minutes depending on connection
- The script shows download progress for large files

### Commercial Use
- Commercial users must license COSMIC through QIAGEN
- Contact: cosmic-translation@sanger.ac.uk
- Academic access is free but requires registration

## Integration with Other Tools

COSMIC data integrates well with:
- **Variant annotation**: VEP, ANNOVAR, SnpEff
- **Signature analysis**: SigProfiler, deconstructSigs, MuSiCa
- **Cancer genomics**: cBioPortal, OncoKB, CIViC
- **Bioinformatics**: Bioconductor, TCGA analysis tools
- **Data science**: pandas, scikit-learn, PyTorch

## Citation

When using COSMIC data, cite:
Tate JG, Bamford S, Jubb HC, et al. COSMIC: the Catalogue Of Somatic Mutations In Cancer. Nucleic Acids Research. 2019;47(D1):D941-D947.
