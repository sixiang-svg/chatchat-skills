---
id: medchem
name: Medchem
description: Medicinal chemistry filters for drug-likeness rules (Lipinski, Veber), PAINS, structural alerts, and complexity metrics.
category: Research
requires: []
examples:
  - Filter this compound library using Lipinski's Rule of Five.
  - Identify PAINS structural alerts in this list of SMILES strings.
---

# Medchem

## Overview

Medchem is a Python library for molecular filtering and prioritization in drug discovery workflows. Apply hundreds of well-established and novel molecular filters, structural alerts, and medicinal chemistry rules to efficiently triage and prioritize compound libraries at scale. Rules and filters are context-specific—use as guidelines combined with domain expertise.

## When to Use This Skill

This skill should be used when:
- Applying drug-likeness rules (Lipinski, Veber, etc.) to compound libraries
- Filtering molecules by structural alerts or PAINS patterns
- Prioritizing compounds for lead optimization
- Assessing compound quality and medicinal chemistry properties
- Detecting reactive or problematic functional groups
- Calculating molecular complexity metrics

## Installation

## Core Capabilities

### 1. Medicinal Chemistry Rules

Apply established drug-likeness rules to molecules using the `medchem.rules` module.

**Available Rules:**
- Rule of Five (Lipinski)
- Rule of Oprea
- Rule of CNS
- Rule of leadlike (soft and strict)
- Rule of three
- Rule of Reos
- Rule of drug
- Rule of Veber
- Golden triangle
- PAINS filters

**Single Rule Application:**


**Multiple Rules with RuleFilters:**


**Result Format:**
Results are returned as dictionaries with pass/fail status and detailed information for each rule.

### 2. Structural Alert Filters

Detect potentially problematic structural patterns using the `medchem.structural` module.

**Available Filters:**

1. **Common Alerts** - General structural alerts derived from ChEMBL curation and literature
2. **NIBR Filters** - Novartis Institutes for BioMedical Research filter set
3. **Lilly Demerits** - Eli Lilly's demerit-based system (275 rules, molecules rejected at >100 demerits)

**Common Alerts:**


**NIBR Filters:**

**Lilly Demerits:**


### 3. Functional API for High-Level Operations

The `medchem.functional` module provides convenient functions for common workflows.

**Quick Filtering:**

### 4. Chemical Groups Detection

Identify specific chemical groups and functional groups using `medchem.groups`.

**Available Groups:**
- Hinge binders
- Phosphate binders
- Michael acceptors
- Reactive groups
- Custom SMARTS patterns

### 5. Named Catalogs

Access curated collections of chemical structures through `medchem.catalogs`.

**Available Catalogs:**
- Functional groups
- Protecting groups
- Common reagents
- Standard fragments


### 6. Molecular Complexity

Calculate complexity metrics that approximate synthetic accessibility using `medchem.complexity`.

**Common Metrics:**
- Bertz complexity
- Whitlock complexity
- Barone complexity

### 7. Constraints Filtering

Apply custom property-based constraints using `medchem.constraints`.

**Example Constraints:**
- Molecular weight ranges
- LogP bounds
- TPSA limits
- Rotatable bond counts

### 8. Medchem Query Language

Use a specialized query language for complex filtering criteria.

**Query Examples:**
```
# Molecules passing Ro5 AND not having common alerts
"rule_of_five AND NOT common_alerts"

# CNS-like molecules with low complexity
"rule_of_cns AND complexity < 400"

# Leadlike molecules without Lilly demerits
"rule_of_leadlike AND lilly_demerits == 0"
```


## Workflow Patterns

### Pattern 1: Initial Triage of Compound Library

Filter a large compound collection to identify drug-like candidates.

### Pattern 2: Lead Optimization Filtering

Apply stricter criteria during lead optimization.

### Pattern 3: Identify Specific Chemical Groups

Find molecules containing specific functional groups or scaffolds.


## Best Practices

1. **Context Matters**: Don't blindly apply filters. Understand the biological target and chemical space.

2. **Combine Multiple Filters**: Use rules, structural alerts, and domain knowledge together for better decisions.

3. **Use Parallelization**: For large datasets (>1000 molecules), always use `n_jobs=-1` for parallel processing.

4. **Iterative Refinement**: Start with broad filters (Ro5), then apply more specific criteria (CNS, leadlike) as needed.

5. **Document Filtering Decisions**: Track which molecules were filtered out and why for reproducibility.

6. **Validate Results**: Remember that marketed drugs often fail standard filters—use these as guidelines, not absolute rules.

7. **Consider Prodrugs**: Molecules designed as prodrugs may intentionally violate standard medicinal chemistry rules.

## Output

- **Filtering Reports**: Detailed pass/fail status for established drug-likeness rules (e.g., Lipinski's Rule of Five, Veber's rules).
- **Structural Alert Logs**: Identification of problematic substructures, including PAINS, NIBR filters, and Lilly demerit scores.
- **Molecular Metrics**: Calculated complexity indices (Bertz, Whitlock, etc.) and physicochemical properties (LogP, MW, TPSA).
- **Prioritized Compound Lists**: A curated set of molecules that have passed the specified medicinal chemistry triage for lead optimization.
