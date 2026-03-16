---
id: uniprot-database
name: UniProt Database
description: Access UniProt via BioServices to retrieve protein sequences, functional annotations, and structural data.
category: Research
requires: []
examples:
  - Retrieve the protein sequence and functional annotations for the human P53 gene.
  - Search UniProt for proteins related to insulin signaling in mammals.
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
- Formulate precise queries to retrieve protein sequences, functional descriptions, and structural metadata from UniProtKB.
- Access detailed functional annotations, including GO terms, enzyme classifications (EC numbers), and post-translational modifications.
- Perform identifier mapping (e.g., UniProt ID to PDB or Ensembl) to integrate protein data into multi-omics pipelines.
- Retrieve protein-protein interaction evidence and biological pathway memberships to support systems biology research.
- Coordinate bulk downloads of protein datasets for specific taxonomic lineages or functional families.
- Adhere to UniProt API rate limits and best practices for large-scale data retrieval in Python.

## Output
- Formatted protein reports containing sequences, functional annotations, and cross-references.
- Mapped identifier lists and structured protein interaction tables.
- Actionable next steps for protein sequence analysis or structure visualization.

## Core Capabilities

### 1. Protein Analysis

Retrieve protein information, sequences, and functional annotations

### 2. Pathway Discovery and Analysis

Access KEGG pathway information for genes and organisms
### 3. Compound Database Searches

Search and cross-reference compounds across multiple databases

**Common workflow:**
1. Search compound by name in KEGG
2. Extract KEGG compound ID
3. Use UniChem for KEGG → ChEMBL mapping
4. ChEBI IDs are often provided in KEGG entries


### 4. Sequence Analysis

Run BLAST searches and sequence alignments
### 5. Identifier Mapping

Convert identifiers between different biological databases

**Supported mappings (UniProt):**
- UniProtKB ↔ KEGG
- UniProtKB ↔ Ensembl
- UniProtKB ↔ PDB
- UniProtKB ↔ RefSeq


### 6. Gene Ontology Queries

Access GO terms and annotations

### 7. Protein-Protein Interactions

Query interaction databases via PSICQUIC

**Available databases:** MINT, IntAct, BioGRID, DIP, and 30+ others.

## Multi-Service Integration Workflows

BioServices excels at combining multiple services for comprehensive analysis. Common integration patterns:

### Complete Protein Analysis Pipeline

Execute a full protein characterization workflow

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

Control API request behavior

### Error Handling

Wrap service calls in try-except blocks

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
