---
id: pytdc
name: PyTDC
description: Therapeutics Data Commons for AI-ready drug discovery datasets, benchmarks, scaffold splits, and molecular oracles.
category: Research
requires: []
examples:
  - Load an ADME dataset from TDC for property prediction.
  - Evaluate model predictions using the TDC MAE evaluator.
---

# PyTDC (Therapeutics Data Commons)

## Overview

PyTDC is an open-science platform providing AI-ready datasets and benchmarks for drug discovery and development. Access curated datasets spanning the entire therapeutics pipeline with standardized evaluation metrics and meaningful data splits, organized into three categories: single-instance prediction (molecular/protein properties), multi-instance prediction (drug-target interactions, DDI), and generation (molecule generation, retrosynthesis).

## When to Use This Skill

This skill should be used when:
- Working with drug discovery or therapeutic ML datasets
- Benchmarking machine learning models on standardized pharmaceutical tasks
- Predicting molecular properties (ADME, toxicity, bioactivity)
- Predicting drug-target or drug-drug interactions
- Generating novel molecules with desired properties
- Accessing curated datasets with proper train/test splits (scaffold, cold-split)
- Using molecular oracles for property optimization

## Installation & Setup

Install PyTDC using pip:


To upgrade to the latest version:


Core dependencies (automatically installed):
- numpy, pandas, tqdm, seaborn, scikit_learn, fuzzywuzzy

Additional packages are installed automatically as needed for specific features.

## Single-Instance Prediction Tasks

Single-instance prediction involves forecasting properties of individual biomedical entities (molecules, proteins, etc.).

### Available Task Categories

#### 1. ADME (Absorption, Distribution, Metabolism, Excretion)

Predict pharmacokinetic properties of drug molecules.


**Common ADME datasets:**
- Caco2 - Intestinal permeability
- HIA - Human intestinal absorption
- Bioavailability - Oral bioavailability
- Lipophilicity - Octanol-water partition coefficient
- Solubility - Aqueous solubility
- BBB - Blood-brain barrier penetration
- CYP - Cytochrome P450 metabolism

#### 2. Toxicity (Tox)

Predict toxicity and adverse effects of compounds.



**Common toxicity datasets:**
- hERG - Cardiac toxicity
- AMES - Mutagenicity
- DILI - Drug-induced liver injury
- Carcinogens - Carcinogenicity
- ClinTox - Clinical trial toxicity

#### 3. HTS (High-Throughput Screening)

Bioactivity predictions from screening data.


#### 4. QM (Quantum Mechanics)

Quantum mechanical properties of molecules.


#### 5. Other Single Prediction Tasks

- **Yields**: Chemical reaction yield prediction
- **Epitope**: Epitope prediction for biologics
- **Develop**: Development-stage predictions
- **CRISPROutcome**: Gene editing outcome prediction

### Data Format

Single prediction datasets typically return DataFrames with columns:
- `Drug_ID` or `Compound_ID`: Unique identifier
- `Drug` or `X`: SMILES string or molecular representation
- `Y`: Target label (continuous or binary)

## Multi-Instance Prediction Tasks

Multi-instance prediction involves forecasting properties of interactions between multiple biomedical entities.

### Available Task Categories

#### 1. DTI (Drug-Target Interaction)

Predict binding affinity between drugs and protein targets.

**Available datasets:**
- BindingDB_Kd - Dissociation constant (52,284 pairs)
- BindingDB_IC50 - Half-maximal inhibitory concentration (991,486 pairs)
- BindingDB_Ki - Inhibition constant (375,032 pairs)
- DAVIS, KIBA - Kinase binding datasets

**Data format:** Drug_ID, Target_ID, Drug (SMILES), Target (sequence), Y (binding affinity)

#### 2. DDI (Drug-Drug Interaction)

Predict interactions between drug pairs.

Multi-class classification task predicting interaction types. Dataset contains 191,808 DDI pairs with 1,706 drugs.

#### 3. PPI (Protein-Protein Interaction)

Predict protein-protein interactions.

#### 4. Other Multi-Prediction Tasks

- **GDA**: Gene-disease associations
- **DrugRes**: Drug resistance prediction
- **DrugSyn**: Drug synergy prediction
- **PeptideMHC**: Peptide-MHC binding
- **AntibodyAff**: Antibody affinity prediction
- **MTI**: miRNA-target interactions
- **Catalyst**: Catalyst prediction
- **TrialOutcome**: Clinical trial outcome prediction

## Generation Tasks

Generation tasks involve creating novel biomedical entities with desired properties.

### 1. Molecular Generation (MolGen)

Generate diverse, novel molecules with desirable chemical properties.


Use with oracles to optimize for specific properties:

### 2. Retrosynthesis (RetroSyn)

Predict reactants needed to synthesize a target molecule.


Dataset contains 1,939,253 reactions from USPTO database.

### 3. Paired Molecule Generation

Generate molecule pairs (e.g., prodrug-drug pairs).

For detailed oracle documentation and molecular generation workflows, refer to `references/oracles.md` and `scripts/molecular_generation.py`.

## Benchmark Groups

Benchmark groups provide curated collections of related datasets for systematic model evaluation.

### ADMET Benchmark Group

**ADMET Group includes 22 datasets** covering absorption, distribution, metabolism, excretion, and toxicity.

### Other Benchmark Groups

Available benchmark groups include collections for:
- ADMET properties
- Drug-target interactions
- Drug combination prediction
- And more specialized therapeutic tasks

## Data Functions

TDC provides comprehensive data processing utilities organized into four categories.

### 1. Dataset Splits

Retrieve train/validation/test partitions with various strategies:

**Available split strategies:**
- `random`: Random shuffling
- `scaffold`: Scaffold-based (for chemical diversity)
- `cold_drug`, `cold_target`, `cold_drug_target`: For DTI tasks
- `temporal`: Time-based splits for temporal datasets

### 2. Model Evaluation

Use standardized metrics for evaluation:

**Available metrics:** ROC-AUC, PR-AUC, F1, Accuracy, RMSE, MAE, R2, Spearman, Pearson, and more.

### 3. Data Processing

TDC provides 11 key processing utilities:

**Processing utilities include:**
- Molecule format conversion (SMILES, SELFIES, PyG, DGL, ECFP, etc.)
- Molecule filters (PAINS, drug-likeness)
- Label binarization and unit conversion
- Data balancing (over/under-sampling)
- Negative sampling for pair data
- Graph transformation
- Entity retrieval (CID to SMILES, UniProt to sequence)


### 4. Molecule Generation Oracles

TDC provides 17+ oracle functions for molecular optimization:


## Advanced Features

### Retrieve Available Datasets


### Label Transformations

### Database Queries

## Common Workflows

### Workflow 1: Train a Single Prediction Model

### Workflow 2: Benchmark Evaluation

### Workflow 3: Molecular Generation with Oracles
