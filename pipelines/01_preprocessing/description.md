## Purpose
Preprocessing prepares raw Sentinel-1 SLC data for interferometric analysis by reducing data volume, correcting orbital geometry, and standardizing the image extent. This step improves computational efficiency and ensures consistency across subsequent InSAR processing stages such as co-registration and interferogram formation.

## Input
- Raw Sentinel-1 SLC products (IW mode)
- Area of interest (AOI) definition

## Reduce Image Size
We will do this using:
- Subset (crop area)
- Multilooking
- Optional coherence mask？

## Output
- Orbit-corrected SLC data
- Spatially cropped SLC images limited to the study area
- Reduced image size suitable for efficient interferometric processing

## Key considerations
- Applying precise orbits improves geometric accuracy and phase quality
- Subsetting should balance computational efficiency with sufficient spatial coverage of deformation signals
- Early data reduction is critical, as large SLC dimensions significantly
  increase interferogram generation and phase unwrapping runtime



- SNAP graph.xml
- preview.png