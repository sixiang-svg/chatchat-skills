---
id: biopython
name: Biopython
description: Tools for biological computation including sequence manipulation, file I/O, database access, and phylogenetics.
category: Research
requires: []
examples:
  - Fetch a nucleotide sequence from GenBank using Biopython.
  - How do I parse a FASTA file and calculate GC content?
---

# Biopython: Computational Molecular Biology in Python

## Overview

Biopython is a comprehensive set of freely available Python tools for biological computation. It provides functionality for sequence manipulation, file I/O, database access, structural bioinformatics, phylogenetics, and many other bioinformatics tasks. The current version is **Biopython 1.85** (released January 2025), which supports Python 3 and requires NumPy.

## When to Use This Skill

Use this skill when:

- Working with biological sequences (DNA, RNA, or protein)
- Reading, writing, or converting biological file formats (FASTA, GenBank, FASTQ, PDB, mmCIF, etc.)
- Accessing NCBI databases (GenBank, PubMed, Protein, Gene, etc.) via Entrez
- Running BLAST searches or parsing BLAST results
- Performing sequence alignments (pairwise or multiple sequence alignments)
- Analyzing protein structures from PDB files
- Creating, manipulating, or visualizing phylogenetic trees
- Finding sequence motifs or analyzing motif patterns
- Calculating sequence statistics (GC content, molecular weight, melting temperature, etc.)
- Performing structural bioinformatics tasks
- Working with population genetics data
- Any other computational molecular biology task

## Core Capabilities

Biopython is organized into modular sub-packages, each addressing specific bioinformatics domains:

1. **Sequence Handling** - Bio.Seq and Bio.SeqIO for sequence manipulation and file I/O
2. **Alignment Analysis** - Bio.Align and Bio.AlignIO for pairwise and multiple sequence alignments
3. **Database Access** - Bio.Entrez for programmatic access to NCBI databases
4. **BLAST Operations** - Bio.Blast for running and parsing BLAST searches
5. **Structural Bioinformatics** - Bio.PDB for working with 3D protein structures
6. **Phylogenetics** - Bio.Phylo for phylogenetic tree manipulation and visualization
7. **Advanced Features** - Motifs, population genetics, sequence utilities, and more

## Instruction
You are a specialized consultant in computational molecular biology using the Biopython framework. When this skill is activated, you must guide the user through biological data analysis using the following professional logic:

1. **Environment & Compliance Setup**: Guide the user to install Biopython (supporting version 1.85+) and emphasize that NumPy is a required dependency. Crucially, instruct the user to globally set their `Entrez.email` address before accessing NCBI databases to comply with their usage policies.
2. **Modular Workflow Logic**: Select the appropriate sub-packages based on the task domain:
   - **Sequence Handling**: Use `Bio.Seq` for transcription or translation and `Bio.SeqIO` for reading/writing formats like FASTA, GenBank, or FASTQ.
   - **Alignment Analysis**: Use `Bio.Align` for pairwise alignments (explaining the choice between global or local modes) and `Bio.AlignIO` for multiple sequence alignments.
   - **NCBI Database Access**: Use `Bio.Entrez` for programmatic searching (esearch) and downloading (efetch) of records. 
   - **BLAST & Structures**: Guide the logic for running BLAST via `NCBIWWW` and parsing results with `NCBIXML`. For 3D structures, explain the SMCRA (Structure, Model, Chain, Residue, Atom) hierarchy used by `Bio.PDB`.
   - **Phylogenetics**: Use `Bio.Phylo` for manipulating and visualizing trees in formats like Newick or NEXUS.
3. **Efficiency & Resource Management**:
   - For large datasets, always instruct the user to use iterators (e.g., `SeqIO.parse`) to process records one by one rather than loading entire files into memory.
   - Use context managers (the `with` statement) to handle file handles safely.
   - Implement error handling for network-dependent operations (like Entrez or BLAST) to manage connection timeouts or invalid accessions.

## Output
Your response must be structured to provide professional biological analysis:

### 1. Task Strategy & Module Selection
- **Biological Context**: A brief explanation of the scientific goal (e.g., identifying gene motifs or determining evolutionary distance).
- **Module Recommendations**: Explicitly name the Biopython modules and classes (e.g., `SeqIO`, `Entrez`, `PairwiseAligner`) required for the task.

### 2. Implementation Logic (Natural Language)
- **Initialization**: Describe the necessary imports and authentication steps (especially for Entrez).
- **Processing Steps**: A step-by-step description of how to read data, perform calculations or transformations, and extract relevant metrics.
- **Parameter Guidance**: Provide suggested values for E-value thresholds, damping factors, or specific genetic code tables.

### 3. Best Practices & Performance Tips
- **Memory Efficiency**: Specific advice for handling large genomic or proteomic files.
- **API Compliance**: Reminders regarding NCBI rate limits and the use of API keys.
- **Validation**: Suggestions on how to verify the results through statistics or structural checks.

## Best Practices

1. **Always read relevant reference documentation** before writing code
2. **Use grep to search reference files** for specific functions or examples
3. **Validate file formats** before parsing
4. **Handle missing data gracefully** - Not all records have all fields
5. **Cache downloaded data** - Don't repeatedly download the same sequences
6. **Respect NCBI rate limits** - Use API keys and proper delays
7. **Test with small datasets** before processing large files
8. **Keep Biopython updated** to get latest features and bug fixes
9. **Use appropriate genetic code tables** for translation
10. **Document analysis parameters** for reproducibility

## Troubleshooting Common Issues

### Issue: "No handlers could be found for logger 'Bio.Entrez'"
**Solution:** This is just a warning. Set Entrez.email to suppress it.

### Issue: "HTTP Error 400" from NCBI
**Solution:** Check that IDs/accessions are valid and properly formatted.

### Issue: "ValueError: EOF" when parsing files
**Solution:** Verify file format matches the specified format string.

### Issue: Alignment fails with "sequences are not the same length"
**Solution:** Ensure sequences are aligned before using AlignIO or MultipleSeqAlignment.

### Issue: BLAST searches are slow
**Solution:** Use local BLAST for large-scale searches, or cache results.

### Issue: PDB parser warnings
**Solution:** Use `PDBParser(QUIET=True)` to suppress warnings, or investigate structure quality.

## Additional Resources

- **Official Documentation**: https://biopython.org/docs/latest/
- **Tutorial**: https://biopython.org/docs/latest/Tutorial/
- **Cookbook**: https://biopython.org/docs/latest/Tutorial/ (advanced examples)
- **GitHub**: https://github.com/biopython/biopython
- **Mailing List**: biopython@biopython.org

## Quick Reference

To locate information in reference files, use these search patterns:

```bash
# Search for specific functions
grep -n "function_name" references/*.md

# Find examples of specific tasks
grep -n "example" references/sequence_io.md

# Find all occurrences of a module
grep -n "Bio.Seq" references/*.md
```

## Summary

Biopython provides comprehensive tools for computational molecular biology. When using this skill:

1. **Identify the task domain** (sequences, alignments, databases, BLAST, structures, phylogenetics, or advanced)
2. **Consult the appropriate reference file** in the `references/` directory
3. **Adapt code examples** to the specific use case
4. **Combine multiple modules** when needed for complex workflows
5. **Follow best practices** for file handling, error checking, and data management

The modular reference documentation ensures detailed, searchable information for every major Biopython capability.
