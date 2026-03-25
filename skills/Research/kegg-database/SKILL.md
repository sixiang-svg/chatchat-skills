---
id: kegg-database
name: KEGG Database
description: Programmatic access to KEGG via BioServices for pathway analysis, gene functions, and metabolic cross-referencing.
category: Research
requires: []
examples:
  - Retrieve the metabolic pathway for the human ZAP70 gene from KEGG.
  - Map these compound IDs to their corresponding KEGG pathway identifiers.
---

# BioServices

## Overview

BioServices is a Python package providing programmatic access to approximately 40 bioinformatics web services and databases. Retrieve biological data, perform cross-database queries, map identifiers, analyze sequences, and integrate multiple biological resources in Python workflows. The package handles both REST and SOAP/WSDL protocols transparently.

## When to Use This Skill

This skill should be used when:
- Retrieving protein sequences, annotations, or structures from UniProt, PDB, Pfam
- Analyzing metabolic pathways and gene functions via KEGG or Reactome
- Searching compound databases (ChEBI, ChEMBL, PubChem) for chemical information
- Converting identifiers between different biological databases (KEGG↔UniProt, compound IDs)
- Running sequence similarity searches (BLAST, MUSCLE alignment)
- Querying gene ontology terms (QuickGO, GO annotations)
- Accessing protein-protein interaction data (PSICQUIC, IntactComplex)
- Mining genomic data (BioMart, ArrayExpress, ENA)
- Integrating data from multiple bioinformatics resources in a single workflow

## Instruction
- Utilize the `BioServices` Python client to query KEGG REST services for genes, pathways, and compounds.
- Retrieve specific metabolic pathway maps and their associated interactions using gene symbols or identifiers.
- Perform identifier mapping between KEGG and other biological databases like UniProt or ChEMBL.
- Search for chemical compounds in ChEBI or PubChem and cross-reference them with KEGG metabolic pathways.
- Extract network interaction data for pathways to enable downstream topological analysis with tools like NetworkX.
- Execute batch ID conversion utilities to process large-scale genomic or metabolomic datasets efficiently.

## Core Capabilities

### 1. Protein Analysis

Retrieve protein information, sequences, and functional annotations:

### 2. Pathway Discovery and Analysis

Access KEGG pathway information for genes and organisms:


**Key methods:**
- `lookfor_organism()`, `lookfor_pathway()`: Search by name
- `get_pathway_by_gene()`: Find pathways containing genes
- `parse_kgml_pathway()`: Extract structured pathway data
- `pathway2sif()`: Get protein interaction networks

Reference: `references/workflow_patterns.md` for complete pathway analysis workflows.

### 3. Compound Database Searches

Search and cross-reference compounds across multiple databases:


**Common workflow:**
1. Search compound by name in KEGG
2. Extract KEGG compound ID
3. Use UniChem for KEGG → ChEMBL mapping
4. ChEBI IDs are often provided in KEGG entries


### 4. Sequence Analysis

Run BLAST searches and sequence alignments:

**Note:** BLAST jobs are asynchronous. Check status before retrieving results.

### 5. Identifier Mapping

Convert identifiers between different biological databases:


### 6. Gene Ontology Queries

Access GO terms and annotations:


### 7. Protein-Protein Interactions


**Available databases:** MINT, IntAct, BioGRID, DIP, and 30+ others.

## Multi-Service Integration Workflows

BioServices excels at combining multiple services for comprehensive analysis. Common integration patterns:

### Complete Protein Analysis Pipeline

Execute a full protein characterization workflow:


This script demonstrates:
1. UniProt search for protein entry
2. FASTA sequence retrieval
3. BLAST similarity search
4. KEGG pathway discovery
5. PSICQUIC interaction mapping

### Pathway Network Analysis

Analyze all pathways for an organism:

Extracts and analyzes:
- All pathway IDs for organism
- Protein-protein interactions per pathway
- Interaction type distributions
- Exports to CSV/SIF formats

### Cross-Database Compound Search

Map compound identifiers across databases:

Retrieves:
- KEGG compound ID
- ChEBI identifier
- ChEMBL identifier
- Basic compound properties

### Batch Identifier Conversion

Convert multiple identifiers at once:


## Best Practices

### Output Format Handling

Different services return data in various formats:
- **XML**: Parse using BeautifulSoup (most SOAP services)
- **Tab-separated (TSV)**: Pandas DataFrames for tabular data
- **Dictionary/JSON**: Direct Python manipulation
- **FASTA**: BioPython integration for sequence analysis

### Rate Limiting and Verbosity

Control API request behavior:


### Error Handling

Wrap service calls in try-except blocks:


### Organism Codes

Use standard organism abbreviations:
- `hsa`: Homo sapiens (human)
- `mmu`: Mus musculus (mouse)
- `dme`: Drosophila melanogaster
- `sce`: Saccharomyces cerevisiae (yeast)

List all organisms: `k.list("organism")` or `k.organismIds`

### Integration with Other Tools

BioServices works well with:
- **BioPython**: Sequence analysis on retrieved FASTA data
- **Pandas**: Tabular data manipulation
- **PyMOL**: 3D structure visualization (retrieve PDB IDs)
- **NetworkX**: Network analysis of pathway interactions
- **Galaxy**: Custom tool wrappers for workflow platforms

## Output
- Formatted reports on gene functions, pathway memberships, and compound properties.
- Network interaction files and metabolic maps for the queried biological entities.
- Automated Python scripts for bulk data retrieval and identifier conversion.
