## Preprocess

`python: 3.11`

(1) convert neuroimaging data from the DICOM format to the NIfTI format

install [dcm2niix](https://github.com/rordenlab/dcm2niix)
```shell
python -m pip install dcm2niix
```

convert neuroimaging data
```shell
dcm2niix -z y -o <target_dir> <data_dir>
```
for example
```shell
dcm2niix -z y -o 3323_niigz 3323_DTI
```
where `3323_DTI` is extracted from `3323_DTI.zip`

(2) Between-volumes Motion Correction on DWI datasets

install [dipy](https://dipy.org/)
```shell
pip install dipy==1.7.0
```
DTI original image data：
![ori.png](3323_niigz%2Fori.png)

After motion correction：
![motion_correction.png](3323_niigz%2Fmotion_correction.png)

code: refer to [motion_correction.ipynb](motion_correction.ipynb)

(3) TODO: Eddy current correction

ECMOCO Tool: http://www.diffusiontools.com/documentation/ECMOCO.html

eddymotion Package: https://github.com/nipreps/eddymotion

FSL Tool: https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/eddy

## Compute Free-Water Maps: 

(1) Estimate free-water maps: Utilize appropriate algorithms (e.g., Free-Water Elimination, FWE) to estimate the presence of free water in each voxel. Free water refers to the cerebrospinal fluid (CSF) component in the brain, which has isotropic diffusion characteristics.

(2) Generate free-water maps: Generate maps that represent the volume fraction of free water in each voxel, indicating the contribution of free water in the diffusion signal at that location.

model convergence:
![loss.png](result_pic%2Floss.png)

Free-Water Maps:
![free_water_map.png](result_pic%2Ffree_water_map.png)

## Free-Water Correction:

(1) Correct DTI metrics for free water: Using the estimated free-water maps, apply corrections to the DTI metrics (FA, MD, etc.) to eliminate the effects of free water contamination.

(2) Obtain free-water corrected DTI metrics: The corrected DTI metrics represent diffusion properties in the brain tissue, excluding the effects of free water.

Mean Diffusivity (free water corrected):
![free_water_corrected.png](result_pic%2Ffree_water_corrected.png)

Fractional Anisotropy (free water corrected):
![free_water_corrected_fa.png](result_pic%2Ffree_water_corrected_fa.png)

code: refer to [example_customized.ipynb](example_customized.ipynb)

