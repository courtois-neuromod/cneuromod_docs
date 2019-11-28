# Derivatives

The Courtois NeuroMod data release includes the output of standard analysis pipelines. Available imaging derivatives are listed below.

## fMRIPrep

The functional data was preprocessed using the fMRIprep pipeline [version: 1.5.0](https://fmriprep.readthedocs.io/en/stable/installation.html). FmriPrep is an fMRI data preprocessing pipeline that requires minimal user input, while providing error and output reporting. It performs basic processing steps (coregistration, normalization, unwarping, noise component extraction, segmentation, skullstripping etc.) and provides outputs that can be easily submitted to a variety of group level analyses, including task-based or resting-state fMRI, graph theory measures, surface or volume-based statistics, etc. The fmriprep pipeline uses a combination of tools from well-known software packages, including FSL, ANTs, FreeSurfer and [AFNI](https://afni.nimh.nih.gov/). This pipeline was designed to provide the best software implementation for each state of preprocessing, although NeuroMod data will be processed with the same fixed version of fMRIprep throughout the project. For additional information fMRIPrep's installion process, it's pipeline, or it's outputs, please visit it's documentation pages [here]https://fmriprep.readthedocs.io/en/stable/installation.html.
 Note that the `slicetiming` and `recon-all` options were disabled (i.e. fMRIprep was invoked with the flags `--fs-no-reconall --ignore slicetiming`).

The outputs of fMRIprep can be found under the folder of each dataset (e.g. `movie10`) `derivatives/fmriprep` in the Courtois NeuroMod datalad. The description of participant, session, task and event tags can be found in the [Datasets](DATASETS.html) section. Each participant folder (`sub-*`) contains:
- `anat` folder with T1 preprocessed and segmented in native and MNI space, registration parameters
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `_boldref.nii.gz` : a BOLD single volume reference.
  - `_*-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `_*-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `_*-confounds_regressors.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM). Note that regressors are likely correlated, thus it is recommended to use a subset of these regressors. Also note that preprocessed time series have not been corrected for any confounds, but simply realigned in space, and it is therefore critical to regress some of the available confounds prior to analysis.For python users, we recommend using this tool [fmriprep_confound_loader](https://github.com/SIMEXP/fmriprep_confound_loader) to load confounds from the fMRIprep outputs, using with the `minimal` strategy. In particular, as the NeuroMod data consistently exhibits low levels of motion, we recommend against removing time points with excessive motion (aka scrubbing).
