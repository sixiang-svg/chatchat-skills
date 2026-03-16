---
id: usgs-data-download
name: USGS Data Download
description: Step-by-step guidance for USGS data download workflows and EarthExplorer best practices.
category: Research
requires: []
examples:
  - How do I download earthquake data from the USGS API?
  - Provide a step-by-step guide for fetching satellite imagery from EarthExplorer.
---

# USGS Data Download

Support usgs data download workflows with clear steps and best practices.

## Instruction
- Define the research area using geographic coordinates (bounding box or point radius) and specify the temporal range.
- Select the appropriate USGS dataset for the task, such as Earthquake catalogs, Landsat satellite imagery, or hydrologic data.
- Utilize the USGS API or EarthExplorer machine-to-machine interface to query available records based on metadata filters.
- Coordinate bulk download requests, managing authentication and handling large data transfers via specialized download managers.
- Extract and validate file metadata to ensure data integrity and proper versioning for scientific analysis.
- Implement automated workflows for periodic data fetching to monitor real-time geological or environmental changes.

## When to Use
- When requiring official geological, hydrological, or remote sensing data for scientific research.
- When automating the retrieval of global earthquake alerts or historical seismic catalogs.
- When performing environmental monitoring or land-use analysis using standardized satellite imagery.

## Output
- A curated download manifest with direct links to the requested USGS data products.
- Structured summaries of identified records including spatial bounds and data quality indicators.
- Actionable steps for data decompression and initial processing in GIS or analysis tools.