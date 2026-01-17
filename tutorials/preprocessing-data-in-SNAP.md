
### Software: SNAP v13
**Note: Be aware of the version of the SNAP you are using. V13 provides new functions that can help saving some manual work, like split, apply orbit etc.**

## Steps (SLC → Coregistration → Interferogram → Filtering → Unwrapping → Geocoding → Displacement) 
1. Open manifest.safe
2. Coregistration: Radar → Coregistration → S1 TOPS Coregistration → S1 TOPS Coregistration
   - Read: YOUR PRE- SLC FILE
   - Read2: YOUR POST- SLC FILE
   - Same apply to Split and Orbit settings 
  <img width="1300" height="409" alt="image" src="https://github.com/user-attachments/assets/86225f5f-b669-4eae-be21-85e1537e0c29" />
  <img width="1184" height="729" alt="image" src="https://github.com/user-attachments/assets/f2c18fb4-e6e0-42fe-ba65-4c8769b37f89" />
  <img width="999" height="91" alt="image" src="https://github.com/user-attachments/assets/85c49ee8-806e-432e-a490-6a85ec35ca99" />

3. Interferogram formation: Radar → Interferometric → Products → Interferogram Formation
  <img width="1506" height="492" alt="image" src="https://github.com/user-attachments/assets/71ab9155-b6a0-41e0-a9c5-5be0487e3bbe" />
  <img width="1023" height="89" alt="image" src="https://github.com/user-attachments/assets/6d6a7c7f-060a-4656-8fa0-b882ce241532" />

4. TOPS Deburst (MANDATORY for Sentinel-1): Radar → Sentinel-1 TOPS → Deburst
  <img width="1139" height="486" alt="image" src="https://github.com/user-attachments/assets/e55d7bca-fda0-4715-a1c2-67a97fa21e0b" />
  <img width="1022" height="76" alt="image" src="https://github.com/user-attachments/assets/4f38cf72-bbbb-45f6-8fce-789e4bb4c21d" />

5. Phase filtering: Radar → Interferometric → Filtering → Goldstein Phase Filtering

6. Phase unwrapping: Radar → Interferometric → Unwrapping → SNAPHU

7. Terrain correction (Geocoding): Radar → Geometric → Terrain Correction → Range-Doppler




### Manual steps for S-1 split, and apply orbit 
**Note: v13 forces you split before orbit, otherwise will get error.**
1. Select the file, Radar - Sentinel-1 TOPS - S1 TOPS Split
   - Sub-swath: IW2 
   - Polarization: VV
   - Burst: default
   <img width="1480" height="693" alt="image" src="https://github.com/user-attachments/assets/dbfb48ff-73d4-4914-ad12-25be9ea30759" />
2. Select the new file ends with 'split', Radar - Apply Orbit File
   Orbit type: Precise with Auto-download
    <img width="1062" height="242" alt="image" src="https://github.com/user-attachments/assets/1f056241-93ff-45fe-9e35-86bd254dacf3" />
