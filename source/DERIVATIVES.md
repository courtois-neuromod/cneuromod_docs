# Derivatives

This is the part of the data that you will likely be interested to feed in your analyses.

## Anatomical preprocessing

### HCPPipelines

The HCPPipelines includes sophisticated combined preprocessing of the T1 and T2 anatomical images to perform accurate volume-based and surface-based segmentation of the participant's brain, using a combination of Ants, Freesurfer, FSL, and include gradient distortion using scanner specific coefficients using [gradunwarp](https://github.com/Washington-University/gradunwarp) (the coefficients cannot be shared due to Manufacturer policy).

## fMRI preprocessing

We are developing a tool [fmriprep_confound_loader](https://github.com/SIMEXP/fmriprep_confound_loader) to load confounds from preprocessing pipeline outputs (fmriprep only for now).

### fMRIPrep

Version: 1.5.0

Options: slicetiming was skipped.

The output can be found in `derivatives/fmriprep`, each participant folder (`sub-*`) contains:

- `anat` folder with T1 preprocessed and segmented in native and MNI space, registration parameters
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `_boldref.nii.gz` : a BOLD single volume reference
  - `_desc-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `_desc-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `_desc-confounds_regressors.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM). Note that regressors are likely correlated, and it is recommended to use a subset of that or a decomposition.


### HCPPipelines
