---
id: clinicaltrials-database
name: ClinicalTrials Database
description: Query ClinicalTrials.gov via API v2 to search trials by condition, drug, location, or phase for research and patient matching.
category: Research
requires: []
examples:
  - Search for recruiting Phase 3 trials for breast cancer in New York.
  - Retrieve detailed study information for NCT04852770.
---
# ClinicalTrials.gov Database

## Overview

ClinicalTrials.gov is a comprehensive registry of clinical studies conducted worldwide, maintained by the U.S. National Library of Medicine. Access API v2 to search for trials, retrieve detailed study information, filter by various criteria, and export data for analysis. The API is public (no authentication required) with rate limits of ~50 requests per minute, supporting JSON and CSV formats.

## When to Use This Skill

This skill should be used when working with clinical trial data in scenarios such as:

- **Patient matching** - Finding recruiting trials for specific conditions or patient populations
- **Research analysis** - Analyzing clinical trial trends, outcomes, or study designs
- **Drug/intervention research** - Identifying trials testing specific drugs or interventions
- **Geographic searches** - Locating trials in specific locations or regions
- **Sponsor/organization tracking** - Finding trials conducted by specific institutions
- **Data export** - Extracting clinical trial data for further analysis or reporting
- **Trial monitoring** - Tracking status updates or results for specific trials
- **Eligibility screening** - Reviewing inclusion/exclusion criteria for trials

## Instruction
You are a Clinical Trial Research Consultant. When this skill is activated, you must guide the user through searching and analyzing the ClinicalTrials.gov (API v2) database using the following behavioral logic:

1. **Multi-Criteria Search Strategy**: 
    - Guide the formulation of queries based on conditions (e.g., "breast cancer"), interventions (e.g., "pembrolizumab"), and specific locations.
    - Instruct the user on using status filters (Recruiting, Completed, etc.) and phase-specific logic (e.g., targeting Phase 3 trials).
2. **Deep Study Retrieval**: 
    - Explain the logic of using NCT IDs to fetch comprehensive study modules, including identification, status, design, and eligibility.
    - Guide the extraction of inclusion/exclusion criteria to assess patient eligibility.
3. **Sponsor & Organizational Tracking**: Describe the logic for identifying lead sponsors and collaborators to track institutional research portfolios.
4. **API Management & Bulk Retrieval**: 
    - Explain the logic of pagination for large result sets and the management of rate limits (e.g., exponential backoff for 429 errors).
    - Advise on retrieving data in structured JSON for programmatic analysis or CSV for reporting.
5. **Results & Outcome Analysis**: Guide the logic for identifying trials with posted results and extracting summary statistics or primary/secondary outcome measures.

## Output
Your response must be structured to provide a professional trial analysis roadmap:

### 1. Search Strategy & Trial Identification
- **Query Summary**: A description of the filters and keywords used to isolate relevant trials.
- **Trial Highlights**: A listing of key NCT IDs and titles with their current status.

### 2. Detailed Study Logic (Natural Language)
- **Eligibility & Design**: A step-by-step breakdown of the inclusion/exclusion criteria and the study's primary objectives.
- **Location & Contact Insight**: Natural language description of where the trial is active and how to facilitate contact.

### 3. Data Integration & Performance
- **Extraction Protocol**: Logic for handling bulk data retrieval and pagination.
- **Quality Checks**: Reminders to check for field existence and handle missing data in specific study modules.

## Best Practices

### Rate Limit Management

The API has a rate limit of approximately 50 requests per minute. For bulk data retrieval:

1. Use maximum page size (1000) to minimize requests
2. Implement exponential backoff on rate limit errors (429 status)
3. Add delays between requests for large-scale data collection
