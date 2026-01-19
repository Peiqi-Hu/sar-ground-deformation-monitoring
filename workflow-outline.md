# SAR Ground Deformation Workflow – Conceptual Outline

This document describes the conceptual workflow behind a SAR-based ground deformation analysis pipeline. It focuses on what each step does and why it exists, rather than implementation details.

The goal is to demonstrate understanding of the pipeline logic, even when some steps are still in progress.

## 1. SAR Data Acquisition
* Input data: **Sentinel-1 Single Look Complex (SLC)** 
* SLC data preserves both **amplitude and phase** information comparing to GRD data type. 
* Phase information (in SLC) is essential for interferometry and deformation analysis.

## 2. Preprocessing (Before Coregistration)
Typical operations:
* Orbit correction
* TOPS Split (select subswath and polarization)
* Subsetting / ROI selection

Purpose:
* Reduce data volume
* Focus on a meaningful geographic area
* Improve downstream computational efficiency

Key insight:
> Poor preprocessing (e.g. large ROI) propagates into very large interferograms, making later steps like phase unwrapping impractical.


## 3. Coregistration
* Align two SLC images (pre- and post-) pixel by pixel
* Ensures that each pixel corresponds to the same ground location

Why it matters:
* Any misalignment directly corrupts phase difference calculations


## 4. Interferogram Generation
* Compute the **phase difference** between coregistered SLC pairs
* Output includes:
  * Wrapped phase
  * Coherence

Wrapped phase:
* Phase values are constrained to the range **(-π, π)**
* This wrapping is a mathematical consequence of phase measurement


## 5. Phase Unwrapping (SNAPHU)
Problem:
* Wrapped phase cannot be directly interpreted as physical displacement

Solution:
* **Phase unwrapping** reconstructs a continuous phase surface

Why SNAPHU?
* SNAP does not perform full unwrapping internally
* SNAPHU is a dedicated, external algorithm optimized for:
  * Large datasets
  * Statistical consistency
  * Parallel processing

Workflow:
1. Export wrapped phase and coherence from SNAP
2. Run SNAPHU externally (command line)
3. Import unwrapped phase back into SNAP


## 6. (Future) Deformation Estimation
* Convert unwrapped phase into line-of-sight displacement
* Apply filtering, reference point selection, and geocoding

This step is planned but not yet implemented.


## Current Focus
* Understanding phase unwrapping mechanics
* Debugging SNAP–SNAPHU integration
* Improving preprocessing to manage data size and performance
