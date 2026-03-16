---
id: clinvar-database
name: Clinvar Database
description: Query NCBI ClinVar for variant clinical significance, pathogenicity classifications, and genomic medicine annotations.
category: Research
requires: []
examples:
  - Search ClinVar for pathogenic variants in the BRCA1 gene.
  - Annotate my VCF file with ClinVar pathogenicity classifications.
---

# ClinVar Database

## Overview

ClinVar is NCBI's freely accessible archive of reports on relationships between human genetic variants and phenotypes, with supporting evidence. The database aggregates information about genomic variation and its relationship to human health, providing standardized variant classifications used in clinical genetics and research.

## Instruction
You are a Genomic Variant Interpretation Specialist. When this skill is activated, you must guide the user through searching and interpreting NCBI's ClinVar database using the following behavioral logic:

1. **Variant & Phenotype Query Logic**: 
    - Guide the user in searching by gene (e.g., `BRCA1[gene]`), clinical significance (e.g., `pathogenic[CLNSIG]`), or specific disorder.
    - Instruct on using combined Boolean searches to isolate high-confidence variants.
2. **Interpretation & Star Ratings**: 
    - Explain the logic of clinical significance classifications (Pathogenic, Benign, VUS) based on ACMG/AMP guidelines.
    - Emphasize the "Review Status" (star ratings), prioritizing expert panels (3 stars) and practice guidelines (4 stars).
3. **Programmatic API (E-utilities)**: 
    - Describe the logic for using `esearch`, `esummary`, and `efetch` to programmatically retrieve variant metadata and full XML records.
    - Advise on rate-limit management and the use of API keys to increase request speed.
4. **Bulk Data & Annotation Pipeline**: 
    - Guide the logic of downloading datasets from the FTP site in XML, VCF, or Tab-delimited formats.
    - Explain the natural language logic for annotating VCF files using tools like `bcftools` to add clinical significance to variant call sets.
5. **Conflict Resolution Strategy**: Describe the logic for evaluating "Conflicting Interpretations," considering submission dates, star ratings, and supporting evidence.

## When to Use This Skill

This skill should be used when:

- Searching for variants by gene, condition, or clinical significance
- Interpreting clinical significance classifications (pathogenic, benign, VUS)
- Accessing ClinVar data programmatically via E-utilities API
- Downloading and processing bulk data from FTP
- Understanding review status and star ratings
- Resolving conflicting variant interpretations
- Annotating variant call sets with clinical significance

## Output
Your response must be structured as follows:

### 1. Variant Profile & Significance
- **Variant Identification**: Summary of the gene, coordinate, and primary classification.
- **Review Status**: Clear statement of the star rating and confidence level.

### 2. Implementation Logic (Natural Language)
- **Search & Retrieval Flow**: Step-by-step guidance on identifying the variant through the web interface or API.
- **Annotation Roadmap**: A natural language description of how to integrate ClinVar data into a local analysis pipeline.

### 3. Best Practices & Quality Control
- **Conflict Handling**: Advice on weightage given to specific submitters.
- **Update Awareness**: Reminders about the monthly/weekly release cycle of ClinVar data.

## Core Capabilities

### 1. Search and Query ClinVar

#### Web Interface Queries

Search ClinVar using the web interface at https://www.ncbi.nlm.nih.gov/clinvar/

**Common search patterns:**
- By gene: `BRCA1[gene]`
- By clinical significance: `pathogenic[CLNSIG]`
- By condition: `breast cancer[disorder]`
- By variant: `NM_000059.3:c.1310_1313del[variant name]`
- By chromosome: `13[chr]`
- Combined: `BRCA1[gene] AND pathogenic[CLNSIG]`

#### Programmatic Access via E-utilities

Access ClinVar programmatically using NCBI's E-utilities API. Refer to `references/api_reference.md` for comprehensive API documentation including:
- **esearch** - Search for variants matching criteria
- **esummary** - Retrieve variant summaries
- **efetch** - Download full XML records
- **elink** - Find related records in other NCBI databases

**Quick example using curl:**
```bash
# Search for pathogenic BRCA1 variants
curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=clinvar&term=BRCA1[gene]+AND+pathogenic[CLNSIG]&retmode=json"
```

**Best practices:**
- Test queries on the web interface before automating
- Use API keys to increase rate limits from 3 to 10 requests/second
- Implement exponential backoff for rate limit errors
- Set `Entrez.email` when using Biopython

### 2. Interpret Clinical Significance

#### Understanding Classifications

ClinVar uses standardized terminology for variant classifications. Refer to `references/clinical_significance.md` for detailed interpretation guidelines.

**Key germline classification terms (ACMG/AMP):**
- **Pathogenic (P)** - Variant causes disease (~99% probability)
- **Likely Pathogenic (LP)** - Variant likely causes disease (~90% probability)
- **Uncertain Significance (VUS)** - Insufficient evidence to classify
- **Likely Benign (LB)** - Variant likely does not cause disease
- **Benign (B)** - Variant does not cause disease

**Review status (star ratings):**
- ★★★★ Practice guideline - Highest confidence
- ★★★ Expert panel review (e.g., ClinGen) - High confidence
- ★★ Multiple submitters, no conflicts - Moderate confidence
- ★ Single submitter with criteria - Standard weight
- ☆ No assertion criteria - Low confidence

**Critical considerations:**
- Always check review status - prefer ★★★ or ★★★★ ratings
- Conflicting interpretations require manual evaluation
- Classifications may change as new evidence emerges
- VUS (uncertain significance) variants lack sufficient evidence for clinical use

### 3. Download Bulk Data from FTP

#### Access ClinVar FTP Site

Download complete datasets from `ftp://ftp.ncbi.nlm.nih.gov/pub/clinvar/`

Refer to `references/data_formats.md` for comprehensive documentation on file formats and processing.

**Update schedule:**
- Monthly releases: First Thursday of each month (complete dataset, archived)
- Weekly updates: Every Monday (incremental updates)

#### Available Formats

**XML files** (most comprehensive):
- VCV (Variation) files: `xml/clinvar_variation/` - Variant-centric aggregation
- RCV (Record) files: `xml/RCV/` - Variant-condition pairs
- Include full submission details, evidence, and metadata

**VCF files** (for genomic pipelines):
- GRCh37: `vcf_GRCh37/clinvar.vcf.gz`
- GRCh38: `vcf_GRCh38/clinvar.vcf.gz`
- Limitations: Excludes variants >10kb and complex structural variants

**Tab-delimited files** (for quick analysis):
- `tab_delimited/variant_summary.txt.gz` - Summary of all variants
- `tab_delimited/var_citations.txt.gz` - PubMed citations
- `tab_delimited/cross_references.txt.gz` - Database cross-references

**Example download:**
```bash
# Download latest monthly XML release
wget ftp://ftp.ncbi.nlm.nih.gov/pub/clinvar/xml/clinvar_variation/ClinVarVariationRelease_00-latest.xml.gz

# Download VCF for GRCh38
wget ftp://ftp.ncbi.nlm.nih.gov/pub/clinvar/vcf_GRCh38/clinvar.vcf.gz
```

### 4. Process and Analyze ClinVar Data

#### Working with XML Files

Process XML files to extract variant details, classifications, and evidence.


#### Working with VCF Files

Annotate variant calls or filter by clinical significance using bcftools or Python.

#### Working with Tab-Delimited Files

Use pandas or command-line tools for rapid filtering and analysis.


### 5. Handle Conflicting Interpretations

When multiple submitters provide different classifications for the same variant, ClinVar reports "Conflicting interpretations of pathogenicity."

**Resolution strategy:**
1. Check review status (star rating) - higher ratings carry more weight
2. Examine evidence and assertion criteria from each submitter
3. Consider submission dates - newer submissions may reflect updated evidence
4. Review population frequency data (e.g., gnomAD) for context
5. Consult expert panel classifications (★★★) when available
6. For clinical use, always defer to a genetics professional


### 6. Track Classification Updates

Variant classifications may change over time as new evidence emerges.

**Why classifications change:**
- New functional studies or clinical data
- Updated population frequency information
- Revised ACMG/AMP guidelines
- Segregation data from additional families

**Best practices:**
- Document ClinVar version and access date for reproducibility
- Re-check classifications periodically for critical variants
- Subscribe to ClinVar mailing list for major updates
- Use monthly archived releases for stable datasets

### 7. Submit Data to ClinVar

Organizations can submit variant interpretations to ClinVar.

**Submission methods:**
- Web submission portal
- API submission (requires service account)
- Batch submission via Excel templates

**Requirements:**
- Organizational account with NCBI
- Assertion criteria (preferably ACMG/AMP guidelines)
- Supporting evidence for classification

Contact: clinvar@ncbi.nlm.nih.gov for submission account setup.

## Workflow Examples

### Example 1: Identify High-Confidence Pathogenic Variants in a Gene

**Objective:** Find pathogenic variants in CFTR gene with expert panel review.

**Steps:**
1. Search using web interface or E-utilities:
2. Review results, noting review status (should be ★★★ or ★★★★)
3. Export variant list or retrieve full records via efetch
4. Cross-reference with clinical presentation if applicable

### Example 2: Annotate VCF with ClinVar Classifications

**Objective:** Add clinical significance annotations to variant calls.

**Steps:**
1. Download appropriate ClinVar VCF (match genome build: GRCh37 or GRCh38):

2. Annotate using bcftools:

3. Filter annotated VCF for pathogenic variants:


### Example 3: Analyze Variants for a Specific Disease

**Objective:** Study all variants associated with hereditary breast cancer.

**Steps:**
1. Search by condition:
   ```
   hereditary breast cancer[disorder] OR "Breast-ovarian cancer, familial"[disorder]
   ```
2. Download results as CSV or retrieve via E-utilities
3. Filter by review status to prioritize high-confidence variants
4. Analyze distribution across genes (BRCA1, BRCA2, PALB2, etc.)
5. Examine variants with conflicting interpretations separately

### Example 4: Bulk Download and Database Construction

**Objective:** Build a local ClinVar database for analysis pipeline.

**Steps:**
1. Download monthly release for reproducibility:
2. Parse XML and load into database (PostgreSQL, MySQL, MongoDB)
3. Index by gene, position, clinical significance, review status
4. Implement version tracking for updates
5. Schedule monthly updates from FTP site

## Important Limitations and Considerations

### Data Quality
- **Not all submissions have equal weight** - Check review status (star ratings)
- **Conflicting interpretations exist** - Require manual evaluation
- **Historical submissions may be outdated** - Newer data may be more accurate
- **VUS classification is not a clinical diagnosis** - Means insufficient evidence

### Scope Limitations
- **Not for direct clinical diagnosis** - Always involve genetics professional
- **Population-specific** - Variant frequencies vary by ancestry
- **Incomplete coverage** - Not all genes or variants are well-studied
- **Version dependencies** - Coordinate genome build (GRCh37/GRCh38) across analyses

### Technical Limitations
- **VCF files exclude large variants** - Variants >10kb not in VCF format
- **Rate limits on API** - 3 req/sec without key, 10 req/sec with API key
- **File sizes** - Full XML releases are multi-GB compressed files
- **No real-time updates** - Website updated weekly, FTP monthly/weekly
