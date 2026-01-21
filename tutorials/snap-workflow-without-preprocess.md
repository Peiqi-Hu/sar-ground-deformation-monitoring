
### Software: SNAP v13
**Note: Be aware of the version of the SNAP you are using. V13 provides new functions that can help saving some manual work, like split, apply orbit etc.**

## Steps (SLC  → Coregistration → Interferogram → Filtering → Unwrapping → Geocoding → Displacement) 
**Note：** Below are for without preprocess, if you've already done preprocess (with TOPS split and applied orbit), and you follow coregistration step below will get you error 'source product should be multi sub swath slc burst products'. 

1. Open manifest.safe
2. **Coregistration**: Radar → Coregistration → S1 TOPS Coregistration → S1 TOPS Coregistration
   - Read: YOUR PRE- SLC FILE
   - Read2: YOUR POST- SLC FILE
   - Same apply to Split and Orbit settings
   - output file:  `*_Orb_Stack.dim`
     
  <img width="1300" height="409" alt="image" src="https://github.com/user-attachments/assets/86225f5f-b669-4eae-be21-85e1537e0c29" />
  <img width="1184" height="729" alt="image" src="https://github.com/user-attachments/assets/f2c18fb4-e6e0-42fe-ba65-4c8769b37f89" />
  <img width="999" height="91" alt="image" src="https://github.com/user-attachments/assets/85c49ee8-806e-432e-a490-6a85ec35ca99" />

3. **Interferogram formation**: Radar → Interferometric → Products → Interferogram Formation
- output file:  `*_Ifg.dim`
  
   <img width="1506" height="492" alt="image" src="https://github.com/user-attachments/assets/71ab9155-b6a0-41e0-a9c5-5be0487e3bbe" />
  <img width="1023" height="89" alt="image" src="https://github.com/user-attachments/assets/6d6a7c7f-060a-4656-8fa0-b882ce241532" />

4. **TOPS Deburst** (MANDATORY for Sentinel-1): Radar → Sentinel-1 TOPS → Deburst
- output file:  `*_Deb.dim`
  
  <img width="1139" height="486" alt="image" src="https://github.com/user-attachments/assets/e55d7bca-fda0-4715-a1c2-67a97fa21e0b" />
  <img width="1022" height="76" alt="image" src="https://github.com/user-attachments/assets/4f38cf72-bbbb-45f6-8fce-789e4bb4c21d" />

5. **Phase filtering**: Radar → Interferometric → Filtering → Goldstein Phase Filtering
- output file:  `**_Filt.dim`

  <img width="1479" height="444" alt="image" src="https://github.com/user-attachments/assets/dbabc0ff-4915-4991-a997-0ba882c49c76" />
   <img width="1026" height="91" alt="image" src="https://github.com/user-attachments/assets/3c96915d-8c74-4a67-b218-6e7a93865828" />

6. **Phase unwrapping**: Radar → Interferometric → Unwrapping → SNAPHU Export
- output file:  specify the target folder, I named it 'snaphu', after running completed, go to the directory，should see file like `UnwPhase_ifg_IW2_VV_24Sep2025_06Oct2025.snaphu.hdr`
- check if the folder contains `UnwPhase_ifg_IW2_VV_24Sep2025_06Oct2025.snaphu.img`, in my case, it is missing as expected since Export will not auto run the SNAPHU unwrap. Skip to the **Manual Generate Unwrapping img** section below. 

<img width="1403" height="479" alt="image" src="https://github.com/user-attachments/assets/5647c102-af44-4a00-8fe6-1ef0478a8ad6" />
<img width="1026" height="480" alt="image" src="https://github.com/user-attachments/assets/4e4e4107-9778-41e1-ad91-4999664782b9" />
<img width="844" height="341" alt="image" src="https://github.com/user-attachments/assets/a9144d99-1884-40e5-aa4f-8d6e7b44b69a" />

- Radar → Interferometric → Unwrapping → SNAPHU Import (The `UnwPhase_**_.snaphu.hdr`) 
  <img width="1300" height="846" alt="image" src="https://github.com/user-attachments/assets/834eea80-30ee-48fd-9998-a471f2f3efd7" />

<img width="1399" height="458" alt="image" src="https://github.com/user-attachments/assets/b02d7324-189f-418b-8330-12b274577b86" />


7. **Terrain correction (Geocoding)**: Radar → Geometric → Terrain Correction → Range-Doppler


## Manual Generate Unwrapping img 
1. **Missing unwrap.snaphu.img**
   - In case you haven't isntalled snaphu in your system, go to https://step.esa.int/main/snap-supported-plugins/snaphu/ to download the zip.
   - In your powershell, cd to your previous snaphu Export folder which contains .hdr, .img, and snaphu.conf, and run command:  `C:\snaphu\snaphu-v1.4.2_win64\bin\snaphu.exe -f snaphu.conf Phase_ifg_IW2_VV_24Sep2025_06Oct2025.snaphu.img 24478`.
      - For `24478`: can double check using `type phase.hdr | find "samples"` to see samples value
      - 
<img width="1065" height="860" alt="image" src="https://github.com/user-attachments/assets/49592947-4b37-4b3e-a6ce-4734f282bf9c" />
<img width="1700" height="442" alt="image" src="https://github.com/user-attachments/assets/90bf684d-1ca4-43db-8d74-b424a0d9bb01" />


## Manual steps for S-1 split, and apply orbit 
**Note: v13 forces you split before orbit, otherwise will get error.**
1. Select the file, Radar - Sentinel-1 TOPS - S1 TOPS Split
   - Sub-swath: IW2 
   - Polarization: VV
   - Burst: default
   <img width="1480" height="693" alt="image" src="https://github.com/user-attachments/assets/dbfb48ff-73d4-4914-ad12-25be9ea30759" />
2. Select the new file ends with 'split', Radar - Apply Orbit File
   Orbit type: Precise with Auto-download
    <img width="1062" height="242" alt="image" src="https://github.com/user-attachments/assets/1f056241-93ff-45fe-9e35-86bd254dacf3" />
