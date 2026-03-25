---
id: ensembl-database
name: Ensembl Database
description: Query Ensembl REST API for gene annotations, sequences, variant analysis, and comparative genomics across 250+ species.
category: Research
requires: []
examples:
  - Look up the genomic coordinates for the human BRCA2 gene.
  - Retrieve orthologs for a mouse gene across vertebrate species.
---

# Ensembl Database

## Overview

Access and query the Ensembl genome database, a comprehensive resource for vertebrate genomic data maintained by EMBL-EBI. The database provides gene annotations, sequences, variants, regulatory information, and comparative genomics data for over 250 species. Current release is 115 (September 2025).

## When to Use This Skill

This skill should be used when:

- Querying gene information by symbol or Ensembl ID
- Retrieving DNA, transcript, or protein sequences
- Analyzing genetic variants using the Variant Effect Predictor (VEP)
- Finding orthologs and paralogs across species
- Accessing regulatory features and genomic annotations
- Converting coordinates between genome assemblies (e.g., GRCh37 to GRCh38)
- Performing comparative genomics analyses
- Integrating Ensembl data into genomic research pipelines

## Core Capabilities

### 1. Gene Information Retrieval

Query gene data by symbol, Ensembl ID, or external database identifiers.

**Common operations:**
- Look up gene information by symbol (e.g., "BRCA2", "TP53")
- Retrieve transcript and protein information
- Get gene coordinates and chromosomal locations
- Access cross-references to external databases (UniProt, RefSeq, etc.)

### 2. Sequence Retrieval

Fetch genomic, transcript, or protein sequences in various formats (JSON, FASTA, plain text).

**Operations:**
- Get DNA sequences for genes or genomic regions
- Retrieve transcript sequences (cDNA)
- Access protein sequences
- Extract sequences with flanking regions or modifications


### 3. Variant Analysis

Query genetic variation data and predict variant consequences using the Variant Effect Predictor (VEP).

**Capabilities:**
- Look up variants by rsID or genomic coordinates
- Predict functional consequences of variants
- Access population frequency data
- Retrieve phenotype associations


### 4. Comparative Genomics

Perform cross-species comparisons to identify orthologs, paralogs, and evolutionary relationships.

**Operations:**
- Find orthologs (same gene in different species)
- Identify paralogs (related genes in same species)
- Access gene trees showing evolutionary relationships
- Retrieve gene family information


### 5. Genomic Region Analysis

Find all genomic features (genes, transcripts, regulatory elements) in a specific region.

**Use cases:**
- Identify all genes in a chromosomal region
- Find regulatory features (promoters, enhancers)
- Locate variants within a region
- Retrieve structural features

### 6. Assembly Mapping

Convert coordinates between different genome assemblies (e.g., GRCh37 to GRCh38).

## API Best Practices

### Rate Limiting

The Ensembl REST API has rate limits. Follow these practices:

1. **Respect rate limits:** Maximum 15 requests per second for anonymous users
2. **Handle 429 responses:** When rate-limited, check the `Retry-After` header and wait
3. **Use batch endpoints:** When querying multiple items, use batch endpoints where available
4. **Cache results:** Store frequently accessed data to reduce API calls

## Common Workflows

### Workflow 1: Gene Annotation Pipeline

1. Look up gene by symbol to get Ensembl ID
2. Retrieve transcript information
3. Get protein sequences for all transcripts
4. Find orthologs in other species
5. Export results

### Workflow 2: Variant Analysis

1. Query variant by rsID or coordinates
2. Use VEP to predict functional consequences
3. Check population frequencies
4. Retrieve phenotype associations
5. Generate report

### Workflow 3: Comparative Analysis

1. Start with gene of interest in reference species
2. Find orthologs in target species
3. Retrieve sequences for all orthologs
4. Compare gene structures and features
5. Analyze evolutionary conservation
