# SNAP workflow with preprocessed SLC 

## Steps (SLC  → Coregistration → Interferogram → Filtering → Unwrapping → Geocoding → Displacement) 

1. Previous step: `tutorials\preprocess-sar.md`
    - output files: `subset_0_*_split.Orb.dim` and `subset_1_*_split.Orb.dim` 

2. **Coregistration - Back Geocoding**: Radar → Coregistration → S1 TOPS Coregistration → S-1 Back Geocoding
    - Add the two subset files
    - output file:  `*split_Orb_Stack.dim`

    ![back_geocoding](images/back_geocoding.png)

    ![back_geocoding_processing](images/back_geocoding_processing.png)

3.  **Interferogram formation**: Radar → Interferometric → Products → Interferogram Formation
- output file:  `*split_Orb_Stack_Ifg.dim`

4. **Topographic phase removel**: Radar → Interferometric → Products → Topographic Phase Removal
    - 