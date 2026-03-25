---
id: instrument-data-to-allotrope
name: Instrument Data to Allotrope
description: Convert lab instrument outputs (PDF, CSV, Excel) to Allotrope Simple Model (ASM) JSON or flattened CSV for LIMS standardization.
category: Research
requires: []
examples:
  - Convert this Vi-CELL BLU Excel report to ASM JSON format.
  - Standardize this plate reader CSV for a LIMS system upload.
---

# Instrument Data to Allotrope Converter

Convert instrument files into standardized Allotrope Simple Model (ASM) format for LIMS upload, data lakes, or handoff to data engineering teams.

> **Note: This is an Example Skill**
>
> This skill demonstrates how skills can support your data engineering tasks—automating schema transformations, parsing instrument outputs, and generating production-ready code.
>
> **To customize for your organization:**
> - Modify the `references/` files to include your company's specific schemas or ontology mappings
> - Use an MCP server to connect to systems that define your schemas (e.g., your LIMS, data catalog, or schema registry)
> - Extend the `scripts/` to handle proprietary instrument formats or internal data standards
>
> This pattern can be adapted for any data transformation workflow where you need to convert between formats or validate against organizational standards.

## Workflow Overview

1. **Detect instrument type** from file contents (auto-detect or user-specified)
2. **Parse file** using allotropy library (native) or flexible fallback parser
3. **Generate outputs**:
   - ASM JSON (full semantic structure)
   - Flattened CSV (2D tabular format)
   - Python parser code (for data engineer handoff)
4. **Deliver** files with summary and usage instructions

> **When Uncertain:** If you're unsure how to map a field to ASM (e.g., is this raw data or calculated? device setting or environmental condition?), ask the user for clarification. Refer to `references/field_classification_guide.md` for guidance, but when ambiguity remains, confirm with the user rather than guessing.


## Output Format Selection

**ASM JSON (default)** - Full semantic structure with ontology URIs
- Best for: LIMS systems expecting ASM, data lakes, long-term archival
- Validates against Allotrope schemas

**Flattened CSV** - 2D tabular representation
- Best for: Quick analysis, Excel users, systems without JSON support
- Each measurement becomes one row with metadata repeated

**Both** - Generate both formats for maximum flexibility

## Calculated Data Handling

**IMPORTANT:** Separate raw measurements from calculated/derived values.

- **Raw data** → `measurement-document` (direct instrument readings)
- **Calculated data** → `calculated-data-aggregate-document` (derived values)

Calculated values MUST include traceability via `data-source-aggregate-document`:


**Common calculated fields by instrument type:**
| Instrument | Calculated Fields |
|------------|-------------------|
| Cell counter | Viability %, cell density dilution-adjusted values |
| Spectrophotometer | Concentration (from absorbance), 260/280 ratio |
| Plate reader | Concentrations from standard curve, %CV |
| Electrophoresis | DIN/RIN, region concentrations, average sizes |
| qPCR | Relative quantities, fold change |

## Validation

Always validate ASM output before delivering to the user:

**Soft Validation Approach:**
Unknown techniques, units, or sample roles generate **warnings** (not errors) to allow for forward compatibility. If Allotrope adds new values after December 2024, the validator won't block them—it will flag them for manual verification. Use `--strict` mode to treat warnings as errors if you need stricter validation.

**What it checks:**
- Correct technique selection (e.g., multi-analyte profiling vs plate reader)
- Field naming conventions (space-separated, not hyphenated)
- Calculated data has traceability 
- Unique identifiers exist for measurements and calculated values
- Required metadata present
- Valid units and sample roles (with soft validation for unknown values)

## Supported Instruments

| Category | Instruments |
|----------|-------------|
| Cell Counting | Vi-CELL BLU, Vi-CELL XR, NucleoCounter |
| Spectrophotometry | NanoDrop One/Eight/8000, Lunatic |
| Plate Readers | SoftMax Pro, EnVision, Gen5, CLARIOstar |
| ELISA | SoftMax Pro, BMG MARS, MSD Workbench |
| qPCR | QuantStudio, Bio-Rad CFX |
| Chromatography | Empower, Chromeleon |

## Detection & Parsing Strategy

### Tier 1: Native allotropy parsing (PREFERRED)
**Always try allotropy first.** Check available vendors directly:

**When the user provides a file, check if allotropy supports it before falling back to manual parsing.** The `scripts/convert_to_asm.py` auto-detection only covers a subset of allotropy vendors.

### Tier 2: Flexible fallback parsing
**Only use if allotropy doesn't support the instrument.** This fallback:
- Does NOT generate `calculated-data-aggregate-document`
- Does NOT include full traceability
- Produces simplified ASM structure

Use flexible parser with:
- Column name fuzzy matching
- Unit extraction from headers
- Metadata extraction from file structure

### Tier 3: PDF extraction
For PDF-only files, extract tables using pdfplumber, then apply Tier 2 parsing.

## Pre-Parsing Checklist

Before writing a custom parser, ALWAYS:

1. **Check if allotropy supports it** 
2. **Find a reference ASM file**
3. **Review instrument-specific guide** 
4. **Validate against reference** 

## Common Mistakes to Avoid

| Mistake | Correct Approach |
|---------|------------------|
| Manifest as object | Use URL string |
| Lowercase detection types | Use "Absorbance" not "absorbance" |
| "emission wavelength setting" | Use "detector wavelength setting" for emission |
| All measurements in one document | Group by well/sample location |
| Missing procedure metadata | Extract ALL device settings per measurement |

## Code Export for Data Engineers

Generate standalone Python scripts that scientists can hand off:

The exported script:
- Has no external dependencies beyond pandas/allotropy
- Includes inline documentation
- Can run in Jupyter notebooks
- Is production-ready for data pipelines

## File Structure

```
instrument-data-to-allotrope/
├── SKILL.md                          # This file
├── scripts/
│   ├── convert_to_asm.py            # Main conversion script
│   ├── flatten_asm.py               # ASM → 2D CSV conversion
│   ├── export_parser.py             # Generate standalone parser code
│   └── validate_asm.py              # Validate ASM output quality
└── references/
    ├── supported_instruments.md     # Full instrument list with Vendor enums
    ├── asm_schema_overview.md       # ASM structure reference
    ├── field_classification_guide.md # Where to put different field types
    └── flattening_guide.md          # How flattening works
```

## Usage Examples

### Example 1: Vi-CELL BLU file

User: "Convert this cell counting data to Allotrope format"
[uploads viCell_Results.xlsx]

Claude:
1. Detects Vi-CELL BLU (95% confidence)
2. Converts using allotropy native parser
3. Outputs:
   - viCell_Results_asm.json (full ASM)
   - viCell_Results_flat.csv (2D format)
   - viCell_parser.py (exportable code)


### Example 2: Request for code handoff

User: "I need to give our data engineer code to parse NanoDrop files"

Claude:
1. Generates self-contained Python script
2. Includes sample input/output
3. Documents all assumptions
4. Provides Jupyter notebook version


### Example 3: LIMS-ready flattened output

User: "Convert this ELISA data to a CSV I can upload to our LIMS"

Claude:
1. Parses plate reader data
2. Generates flattened CSV with columns:
   - sample_identifier, well_position, measurement_value, measurement_unit
   - instrument_serial_number, analysis_datetime, assay_type
3. Validates against common LIMS import requirements

