# SNAP workflow with preprocessed SLC 

## Steps (SLC  → Coregistration → Interferogram → Filtering → Unwrapping → Geocoding → Displacement) 

1. Previous step: `tutorials\preprocess-sar.md`
    - output files: `subset_0_*_split.Orb.deb.dim` and `subset_1_*_split.Orb.deb.dim` 

2. **Coregistration - Back Geocoding**: Radar → Coregistration → S1 TOPS Coregistration → S-1 Back Geocoding
    - Add the two subset files
    - If Back Geocoding did not read the subset file, you can go back to the Step 1, export or save the product as **BEAM-DIMAP** if you haven't done so. 
    - output file:  `subset_*_split_Orb_deb_Stack.dim` (may have different naming, but should ends with the same)

    ![back_geocoding](images/back_geocoding.png)

    ![back_geocoding_processing](images/back_geocoding_processing.png)

3.  **Interferogram formation**: Radar → Interferometric → Products → Interferogram Formation
    - output file:  `*split_Orb_deb_Stack_Ifg.dim`

4. **Topographic phase removel**: Radar → Interferometric → Products → Topographic Phase Removal
    - This isolates surface deformation + atmosphere + noise. 
    - If you got error saying need deburst file, unfortunetly need to go back to `tutorials\preprocess-sar.md`, starting from Step 4 to do the deburst first.
    - output file:  `*split_Orb_deb_Stack_Ifg_dinsar.dim`

5. **Multilooking**: Radar → SAR Utilities → Multilooking
    - To further reduce resolution if image size is still large.
    - output file:  `*split_Orb_deb_Stack_Ifg_dinsar_ML.dim`

    ![multilooking](images/multilooking.png)

6. **Goldstein Phase Filtering**: Radar → Interferometric → Filtering → Goldstein Phase Filtering
    - output file:  `*split_Orb_deb_Stack_Ifg_dinsar_ML_flt.dim`

7. **SNAPHU Export**: Radar → Interferometric → Unwrapping → Snaphu Export
    - output folder contains below:
        ![snaphu_export_subset](images/snaphu_export_subset.png)

8. **SNAPHU Unwarp**
    - if you haven't install snaphu, go to [Phase Unwarpping with SNAPHU](https://step.esa.int/main/third-party-plugins-2/snaphu/) to download it. 
    - After you completed installation/download, go to your folder path where you export to in Step 7.
    - open `snaphu.conf`, you can find the cmd usually in line 7 under 'command to call snaphu'.
    - `type phase.hdr` to double check the samples value, should match with command
        ![phase_info](images/phase_info.png)

        **Note**: 

        | ENVI field       | snaphu.conf   |
        | ---------------- | ------------- |
        | `samples`        | COLS          |
        | `lines`          | ROWS          |
        | `data type = 4`  | FLOAT         |
        | `byte order = 0` | LITTLE_ENDIAN |
        | `byte order = 1` | BIG_ENDIAN    |

    - run ` snaphu -f snaphu.conf Phase_ifg_VV_24Sep2025_06Oct2025.snaphu.img 1954`.   
    - if got error `Unexpected or abnormal exit of child process 23068
Abort `:
        - Go back to snaphu.conf, under Input Files command out the `CORRFILE .snaphu.img`.

    - run cmd below in powershell: `snaphu.exe -f snaphu.conf Phase_ifg_VV_24Sep2025_06Oct2025.snaphu.img 1954`. If success, should see below:
        ![success_unwrap_snaphu](images/success_unwrap_snaphu.png)

9. **SNAPHU Import**: Radar → Interferometric → Unwrapping → Snaphu Import
