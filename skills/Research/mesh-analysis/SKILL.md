---
id: mesh-analysis
name: Mesh Analysis
description: Step-by-step guidance for 3D mesh analysis workflows, repairing geometry, and surface optimization.
category: Research
requires: []
examples:
  - How do I perform mesh analysis to find non-manifold geometry in this STL?
  - What are the best practices for mesh simplification and surface smoothing?
---

# Mesh Analysis

Support mesh workflows with clear steps and best practices.

## Instruction
- Perform an initial geometry audit to identify errors such as non-manifold edges, self-intersections, and degenerate faces.
- Execute automated mesh repair routines to fill holes, unify normal directions, and remove redundant vertices.
- Apply mesh simplification algorithms (e.g., decimation) to reduce poly-count while preserving critical structural features.
- Utilize smoothing filters to reduce surface noise and improve aesthetic quality for visualization or 3D printing.
- Validate the mesh integrity after each optimization step to ensure it remains "watertight" and suitable for downstream tasks.
- Export the optimized mesh in standard formats (STL, OBJ, PLY) with preserved UV coordinates if necessary.

## When to Use
- When preparing 3D models for additive manufacturing (3D printing) where watertight geometry is required.
- When optimizing high-resolution scan data for real-time rendering or simulation.
- When cleaning up CAD-to-mesh conversions for computational fluid dynamics (CFD) or finite element analysis (FEA).

## Output
- A mesh quality report summarizing identified errors and applied repair actions.
- Optimized and repaired 3D mesh files in the user's requested format.
- Actionable advice for further surface treatment or simulation-ready prep.