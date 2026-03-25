---
id: drugbank-database
name: Drugbank Database
description: Access DrugBank data for drug properties, interactions, targets, pathways, chemical structures, and pharmacology research.
category: Research
requires: []
examples:
  - Find all FDA-approved drug targets for a specific protein.
  - Retrieve drug-drug interaction data for a list of pharmaceutical compounds.
---

# DrugBank Database

## Overview

DrugBank is a comprehensive bioinformatics and cheminformatics database containing detailed information on drugs and drug targets. This skill enables programmatic access to DrugBank data including ~9,591 drug entries (2,037 FDA-approved small molecules, 241 biotech drugs, 96 nutraceuticals, and 6,000+ experimental compounds) with 200+ data fields per entry.

## When to Use
- When accessing DrugBank data for drug properties, interactions, targets, or pathway research.
- When building searchable drug datasets or performing structure-activity relationship (SAR) studies.
- When conducting clinical decision support analysis or pharmacovigilance research involving complex interactions.

## Core Capabilities

### 1. Data Access and Authentication

Download and access DrugBank data using Python with proper authentication. The skill provides guidance on:

- Installing and configuring the `drugbank-downloader` package
- Managing credentials securely via environment variables or config files
- Downloading specific or latest database versions
- Opening and parsing XML data efficiently
- Working with cached data to optimize performance

**When to use**: Setting up DrugBank access, downloading database updates, initial project configuration.


### 2. Drug Information Queries

Extract comprehensive drug information from the database including identifiers, chemical properties, pharmacology, clinical data, and cross-references to external databases.

**Query capabilities**:
- Search by DrugBank ID, name, CAS number, or keywords
- Extract basic drug information (name, type, description, indication)
- Retrieve chemical properties (SMILES, InChI, molecular formula)
- Get pharmacology data (mechanism of action, pharmacodynamics, ADME)
- Access external identifiers (PubChem, ChEMBL, UniProt, KEGG)
- Build searchable drug datasets and export to DataFrames
- Filter drugs by type (small molecule, biotech, nutraceutical)

**When to use**: Retrieving specific drug information, building drug databases, pharmacology research, literature review, drug profiling.

### 3. Drug-Drug Interactions Analysis

Analyze drug-drug interactions (DDIs) including mechanism, clinical significance, and interaction networks for pharmacovigilance and clinical decision support.

**Analysis capabilities**:
- Extract all interactions for specific drugs
- Build bidirectional interaction networks
- Classify interactions by severity and mechanism
- Check interactions between drug pairs
- Identify drugs with most interactions
- Analyze polypharmacy regimens for safety
- Create interaction matrices and network graphs
- Perform community detection in interaction networks
- Calculate interaction risk scores

**When to use**: Polypharmacy safety analysis, clinical decision support, drug interaction prediction, pharmacovigilance research, identifying contraindications.

### 4. Drug Targets and Pathways

Access detailed information about drug-protein interactions including targets, enzymes, transporters, carriers, and biological pathways.

**Target analysis capabilities**:
- Extract drug targets with actions (inhibitor, agonist, antagonist)
- Identify metabolic enzymes (CYP450, Phase II enzymes)
- Analyze transporters (uptake, efflux) for ADME studies
- Map drugs to biological pathways (SMPDB)
- Find drugs targeting specific proteins
- Identify drugs with shared targets for repurposing
- Analyze polypharmacology and off-target effects
- Extract Gene Ontology (GO) terms for targets
- Cross-reference with UniProt for protein data

**When to use**: Mechanism of action studies, drug repurposing research, target identification, pathway analysis, predicting off-target effects, understanding drug metabolism.

### 5. Chemical Properties and Similarity

Perform structure-based analysis including molecular similarity searches, property calculations, substructure searches, and ADMET predictions.

**Chemical analysis capabilities**:
- Extract chemical structures (SMILES, InChI, molecular formula)
- Calculate physicochemical properties (MW, logP, PSA, H-bonds)
- Apply Lipinski's Rule of Five and Veber's rules
- Calculate Tanimoto similarity between molecules
- Generate molecular fingerprints (Morgan, MACCS, topological)
- Perform substructure searches with SMARTS patterns
- Find structurally similar drugs for repurposing
- Create similarity matrices for drug clustering
- Predict oral absorption and BBB permeability
- Analyze chemical space with PCA and clustering
- Export chemical property databases

**When to use**: Structure-activity relationship (SAR) studies, drug similarity searches, QSAR modeling, drug-likeness assessment, ADMET prediction, chemical space exploration.


## Installation Requirements


### Account Setup
1. Create free account at go.drugbank.com
2. Accept license agreement (free for academic use)
3. Obtain username and password credentials
4. Configure credentials 

## Data Version and Reproducibility

Always specify the DrugBank version for reproducible research.

Document the version used in publications and analysis scripts.

## Best Practices

1. **Credentials**: Use environment variables or config files, never hardcode
2. **Versioning**: Specify exact database version for reproducibility
3. **Caching**: Cache parsed data to avoid re-downloading and re-parsing
4. **Namespaces**: Handle XML namespaces properly when parsing
5. **Validation**: Validate chemical structures with RDKit before use
6. **Cross-referencing**: Use external identifiers (UniProt, PubChem) for integration
7. **Clinical Context**: Always consider clinical context when interpreting interaction data
8. **License Compliance**: Ensure proper licensing for your use case
