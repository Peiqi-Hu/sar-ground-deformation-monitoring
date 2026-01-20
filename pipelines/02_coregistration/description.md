## Purpose
Co-registration aligns the pre- and post- SAR images so that each pixel
corresponds to the same ground location. Accurate co-registration is critical because phase differences are computed pixel by pixel in later steps.

## Input
- Two Sentinel-1 SLC images (pre AND post)
- Precise orbit information

## Output
- Co-registered SLC stack with aligned geometry
- file ends with ` .dim`

## Key considerations
- Sub-pixel misalignment can introduce phase noise
- TOPS mode requires burst-level alignment
- Errors here propagate into interferogram quality
