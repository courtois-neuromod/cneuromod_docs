# Derivatives

This is the part of the data that you will likely be interested to feed in your analyses. This page is still undercontruction, but should be completed soon.

## Anatomical preprocessing

### HCP Pipelines 

version 3.1 (WIP)

The HCP Pipelines includes sophisticated combined preprocessing of the T1 and T2 anatomical images to perform accurate volume-based and surface-based segmentation of the participant's brain, using a combination of [ANTs](http://stnava.github.io/ANTs/),  [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/MultiModalTutorialV6.0/IndividualFMRI),[FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki), and include gradient distortion using scanner specific coefficients using [gradunwarp](https://github.com/Washington-University/gradunwarp) (the coefficients cannot be shared due to manufacturer policy).

For additional information on on instalation and prerequisites, please visit their [Documentation and Release Notes](https://github.com/Washington-University/HCPpipelines/wiki/Installation-and-Usage-Instructions).

## fMRI preprocessing

We are developing a tool [fmriprep_confound_loader](https://github.com/SIMEXP/fmriprep_confound_loader) to load confounds from preprocessing pipeline outputs ([fMRIPrep](https://fmriprep.readthedocs.io/en/stable/#) only for now).

### fMRIPrep
 
Version: 1.5.0

XXX Add brief description of fmriprepXX

Options: slicetiming was skipped.

The output can be found in `derivatives/fmriprep`, each participant folder (`sub-*`) contains:

- `anat` folder with T1 preprocessed and segmented in native and MNI space, registration parameters
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `_boldref.nii.gz` : a BOLD single volume reference
  - `_desc-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `_desc-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `_desc-confounds_regressors.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM). Note that regressors are likely correlated, thus it is recommended to use a subset of these regressors or components of an orthogonal decomposition (eg. PCA) that explains a large share of the variance.


### HCP Pipelines

TODO: beta, try to use v4.0 (freesurfer6)
