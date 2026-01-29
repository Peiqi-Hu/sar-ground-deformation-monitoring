# SAR Earthquake Ground Deformation Monitoring

## Overview
This project explores the use of open-access Sentinel-1 Synthetic Aperture Radar (SAR) data to study earthquake-related ground deformation, with a primary focus on understanding and debugging the InSAR processing workflow. The goal is to demonstrate practical knowledge of Earth Observation (EO) pipelines, tool integration, and real-world computational constraints encountered in InSAR-based monitoring applications.

This project is intended as an **educational and analytical demonstration**.

## Current Status & Challenges
- Phase unwrapping integration with SNAPHU (DONE)
- Large interferogram size affecting performance (DONE)
- Improving preprocessing and ROI selection (DONE)
- SNAPHU import file selection (DONE)
- QGIS (In-progress)

## Motivation
Earthquakes cause measurable surface displacement that can impact cities, transportations, pipelines, and other critical infrastructure. Interferometric SAR (InSAR) is a widely used remote sensing technique for detecting and quantifying such ground deformation.

This project was developed to:
- Gain hands-on experience with SAR-based EO data
- Apply signal and image processing concepts to real satellite imagery
- Practice geospatial visualization and analytical communication
- Simulate an analyst-style workflow aligned with operational EO analytics roles


## Data
- **Satellite:** Sentinel-1 (C-band SAR)
- **Source:** Copernicus Open Access Hub / ASF 
- **Acquisition mode:** Interferometric Wide Swath (IW)
- **Images:** Two SAR scenes (SLC) acquired before and after a selected earthquake event
- **Study Area:** Cebu, Philipines - Earthquake happened on Sept.30th, 2025 
- **Orbit:** Same relative orbit to ensure interferometric compatibility

All data used in this project is publicly available.


## Methodology
Overview: `Data acquisition - Preprocessing/subset - Coregistration - Inteferogram - Multilooking - Goldstein filter - Phase export - Phase unwrap (snaphu) - Phase import - cont `

### 0. Guides
- Step-by-step guides for InSAR processing with SNAP are located in `/guides`.
- This folder also includes my project notes and key learnings.
  
### 1. Data Acquisition 
- Selected a real earthquake event and corresponding geographic region
- Downloaded pre-event and post-event Sentinel-1 SAR images
- Ensured consistent acquisition geometry (orbit direction and track)
- see `/guides/data-acquisition.md`

### 2. Preprocessing
- Applied splits and orbit 
- Cropped SAR scenes to the region of interest (subset)
- Visualized SAR intensity to assess data quality
- see `/guides/preprocess-sar.md`

### 3. Interferometric Analysis (Simplified)
- Computed phase differences between pre- and post-event SAR images
- Generated a wrapped interferogram to highlight surface displacement patterns
- Applied basic filtering to reduce noise
- Interpreted fringe patterns as relative ground motion

### 4. Change Detection
- Estimated coherence between SAR image pairs
- Identified low-coherence areas associated with surface change or instability
- Compared deformation behavior across different land cover types (e.g., urban vs non-urban)

### 5. Visualization & Communication
- Produced deformation and coherence maps
- Added clear legends, color scales, and annotations
- Highlighted areas of notable ground displacement
- Summarized findings in analyst-style figures suitable for reporting


## Results
Key outputs include:
- Wrapped interferogram illustrating earthquake-induced surface displacement
- Coherence map indicating stable vs disturbed ground regions
- Geospatial visualizations suitable for infrastructure impact assessment

The results demonstrate how SAR-based EO data can be used to monitor and communicate ground deformation phenomena following seismic events.


## Limitations
- This project uses simplified, open-source processing techniques
- No precise phase unwrapping or atmospheric correction is performed
- Results are qualitative and relative, not absolute displacement measurements
- Operational InSAR systems involve more advanced calibration and validation steps

These limitations are acknowledged to ensure technical transparency.


## Tools & Technologies
- **Programming:** Python
- **Libraries:** NumPy, rasterio, matplotlib, scipy, snaphu
- **Data Type:** SAR raster data
- **Techniques:** Signal processing, interferometry concepts, geospatial visualization


## Repository Structure



## Future Improvements
- Phase unwrapping and displacement scaling
- Atmospheric noise correction
- Integration with GIS tools (e.g., ESRI-compatible outputs)
- Time-series analysis using multiple SAR acquisitions
- Machine learning-based change classification


## Disclaimer
This project is for demonstration and learning purposes only. It does not represent an operational InSAR processing system and should not be used for real-world hazard assessment or decision-making.

