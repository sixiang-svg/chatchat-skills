---
id: zinc-database
name: Zinc Database
description: Access ZINC database for purchasable compounds, similarity searches, and 3D-ready structures for virtual screening.
category: Research
requires: []
examples:
  - Search the ZINC database for analogs of this SMILES string.
  - Download 3D-ready structures for virtual screening from ZINC22.
---

# ZINC Database

## Overview

ZINC is a freely accessible repository of 230M+ purchasable compounds maintained by UCSF. Search by ZINC ID or SMILES, perform similarity searches, download 3D-ready structures for docking, discover analogs for virtual screening and drug discovery.

## When to Use This Skill

This skill should be used when:

- **Virtual screening**: Finding compounds for molecular docking studies
- **Lead discovery**: Identifying commercially-available compounds for drug development
- **Structure searches**: Performing similarity or analog searches by SMILES
- **Compound retrieval**: Looking up molecules by ZINC IDs or supplier codes
- **Chemical space exploration**: Exploring purchasable chemical diversity
- **Docking studies**: Accessing 3D-ready molecular structures
- **Analog searches**: Finding similar compounds based on structural similarity
- **Supplier queries**: Identifying compounds from specific chemical vendors
- **Random sampling**: Obtaining random compound sets for screening

## Instruction
- Identify the target molecules for search using ZINC IDs, supplier codes, or SMILES strings.
- Select the appropriate database version, prioritizing ZINC22 for multi-billion scale tangible compound discovery.
- Perform structure-based searches to find analogs or similar compounds for lead discovery and virtual screening.
- Download 3D-ready molecular structures in SDF or MOL2 formats, ensuring they are prepared for docking workflows.
- Apply filters based on purchasability, molecular weight, and logP to identify leads that meet specific medicinal chemistry criteria.
- Coordinate random sampling of compound sets to build diverse screening libraries for experimental validation.
- Verify supplier information and compound availability through the CartBlanche22 interface or API links.

## Output
- Filtered lists of purchasable compounds with associated ZINC IDs and structural data.
- Download manifests for 3D-ready structures tailored to molecular docking pipelines.
- Summaries of chemical space coverage and identified supplier networks for target leads.

## Best Practices

### Query Optimization

- **Start specific**: Begin with exact searches before expanding to similarity searches
- **Use appropriate distance parameters**: Small dist values (1-3) for close analogs, larger (5-10) for diverse analogs
- **Limit output fields**: Request only necessary fields to reduce data transfer
- **Batch queries**: Combine multiple ZINC IDs in a single API call when possible

### Performance Considerations

- **Rate limiting**: Respect server resources; avoid rapid consecutive requests
- **Caching**: Store frequently accessed compounds locally
- **Parallel downloads**: When downloading 3D structures, use parallel wget or aria2c for file repositories
- **Subset filtering**: Use lead-like, drug-like, or fragment subsets to reduce search space

### Data Quality

- **Verify availability**: Supplier catalogs change; confirm compound availability before large orders
- **Check stereochemistry**: SMILES may not fully specify stereochemistry; verify 3D structures
- **Validate structures**: Use cheminformatics tools (RDKit, OpenBabel) to verify structure validity
- **Cross-reference**: When possible, cross-check with other databases (PubChem, ChEMBL)

## Resources

Comprehensive documentation including:

- Complete API endpoint reference
- URL syntax and parameter specifications
- Advanced query patterns and examples
- File repository organization and access
- Bulk download methods
- Error handling and troubleshooting
- Integration with molecular docking software

Consult this document for detailed technical information and advanced usage patterns.

## Important Disclaimers

### Data Reliability

ZINC explicitly states: **"We do not guarantee the quality of any molecule for any purpose and take no responsibility for errors arising from the use of this database."**

- Compound availability may change without notice
- Structure representations may contain errors
- Supplier information should be verified independently
- Use appropriate validation before experimental work

### Appropriate Use

- ZINC is intended for academic and research purposes in drug discovery
- Verify licensing terms for commercial use
- Respect intellectual property when working with patented compounds
- Follow your institution's guidelines for compound procurement
