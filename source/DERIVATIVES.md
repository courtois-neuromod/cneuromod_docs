# Derivatives

The Courtois NeuroMod data release includes the output of standard analysis pipelines. Available imaging derivatives are listed below.

## fMRIPrep

The functional data was preprocessed using the fMRIprep pipeline [version: 1.5.0](https://fmriprep.readthedocs.io/en/stable/installation.html). FmriPrep is an fMRI data preprocessing pipeline that requires minimal user input, while providing error and output reporting. It performs basic processing steps (coregistration, normalization, unwarping, noise component extraction, segmentation, skullstripping etc.) and provides outputs that can be easily submitted to a variety of group level analyses, including task-based or resting-state fMRI, graph theory measures, surface or volume-based statistics, etc. The fmriprep pipeline uses a combination of tools from well-known software packages, including FSL, ANTs, FreeSurfer and [AFNI](https://afni.nimh.nih.gov/). This pipeline was designed to provide the best software implementation for each state of preprocessing, although NeuroMod data will be processed with the same fixed version of fMRIprep throughout the project. For additional information fMRIPrep's installion process, it's pipeline, or it's outputs, please visit it's documentation pages [here](https://fmriprep.readthedocs.io/en/stable/installation.html).
 Note that the `slicetiming` and `recon-all` options were disabled (i.e. fMRIprep was invoked with the flags `--fs-no-reconall --ignore slicetiming`).

The outputs of fMRIprep can be found under the folder of each dataset (e.g. `movie10`) `derivatives/fmriprep` in the Courtois NeuroMod datalad. The description of participant, session, task and event tags can be found in the [Datasets](DATASETS.html) section. Each participant folder (`sub-*`) contains:
- `anat` folder with T1 preprocessed and segmented in native and MNI space, registration parameters
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `_boldref.nii.gz` : a BOLD single volume reference.
  - `_*-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `_*-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `_*-confounds_regressors.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM). Note that regressors are likely correlated, thus it is recommended to use a subset of these regressors. Also note that preprocessed time series have not been corrected for any confounds, but simply realigned in space, and it is therefore critical to regress some of the available confounds prior to analysis.For python users, we recommend using this tool [fmriprep_confound_loader](https://github.com/SIMEXP/fmriprep_confound_loader) to load confounds from the fMRIprep outputs, using with the `minimal` strategy. In particular, as the NeuroMod data consistently exhibits low levels of motion, we recommend against removing time points with excessive motion (aka scrubbing).

### ** BUG **

The following run's preprocessing are missing because of fMRIPrep issues at the time of the `cneuromod-2020-alpha` release.
This will be fixed for the `cneuromod-2020-beta` release, scheduled in April 2020.

#### Movie-10:

```
sub-05/ses-vid010/func/sub-05_ses-vid010_task-hiddenfigures_run-11_bold.nii.gz
sub-06/ses-vid005/func/sub-06_ses-vid005_task-bournesupremacy_run-02_bold.nii.gz
sub-06/ses-vid005/func/sub-06_ses-vid005_task-life_run-04_bold.nii.gz
sub-06/ses-vid006/func/sub-06_ses-vid006_task-bournesupremacy_run-06_bold.nii.gz
sub-06/ses-vid009/func/sub-06_ses-vid009_task-wolfofwallstreet_run-02_bold.nii.gz
```

#### HCP-trt

```
sub-01/ses-002/func/sub-01_ses-002_task-emotion_run-02_bold.nii.gz
sub-01/ses-003/func/sub-01_ses-003_task-emotion_run-01_bold.nii.gz
sub-01/ses-003/func/sub-01_ses-003_task-language_run-01_bold.nii.gz
sub-01/ses-003/func/sub-01_ses-003_task-social_run-01_bold.nii.gz
sub-01/ses-004/func/sub-01_ses-004_task-gambling_run-01_bold.nii.gz
sub-01/ses-004/func/sub-01_ses-004_task-motor_run-01_bold.nii.gz
sub-01/ses-004/func/sub-01_ses-004_task-restingstate_run-01_bold.nii.gz
sub-01/ses-007/func/sub-01_ses-007_task-emotion_run-01_bold.nii.gz
sub-01/ses-007/func/sub-01_ses-007_task-relational_run-01_bold.nii.gz
sub-01/ses-007/func/sub-01_ses-007_task-social_run-01_bold.nii.gz
sub-01/ses-009/func/sub-01_ses-009_task-language_run-01_bold.nii.gz
sub-01/ses-009/func/sub-01_ses-009_task-relational_run-01_bold.nii.gz
sub-01/ses-010/func/sub-01_ses-010_task-gambling_run-02_bold.nii.gz
sub-01/ses-010/func/sub-01_ses-010_task-motor_run-01_bold.nii.gz
sub-01/ses-010/func/sub-01_ses-010_task-motor_run-02_bold.nii.gz
sub-02/ses-001/func/sub-02_ses-001_task-motor_run-01_bold.nii.gz
sub-02/ses-001/func/sub-02_ses-001_task-relational_run-01_bold.nii.gz
sub-02/ses-003/func/sub-02_ses-003_task-motor_run-01_bold.nii.gz
sub-02/ses-003/func/sub-02_ses-003_task-social_run-01_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-gambling_run-01_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-gambling_run-02_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-language_run-01_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-language_run-02_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-motor_run-01_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-relational_run-02_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-social_run-01_bold.nii.gz
sub-02/ses-004/func/sub-02_ses-004_task-wm_run-02_bold.nii.gz
sub-02/ses-005/func/sub-02_ses-005_task-emotion_run-01_bold.nii.gz
sub-02/ses-005/func/sub-02_ses-005_task-restingstate_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-gambling_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-language_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-relational_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-relational_run-02_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-social_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-wm_run-01_bold.nii.gz
sub-02/ses-006/func/sub-02_ses-006_task-wm_run-02_bold.nii.gz
sub-02/ses-007/func/sub-02_ses-007_task-emotion_run-01_bold.nii.gz
sub-02/ses-007/func/sub-02_ses-007_task-language_run-01_bold.nii.gz
sub-02/ses-008/func/sub-02_ses-008_task-gambling_run-02_bold.nii.gz
sub-02/ses-008/func/sub-02_ses-008_task-language_run-02_bold.nii.gz
sub-02/ses-008/func/sub-02_ses-008_task-motor_run-01_bold.nii.gz
sub-02/ses-008/func/sub-02_ses-008_task-relational_run-01_bold.nii.gz
sub-02/ses-008/func/sub-02_ses-008_task-wm_run-02_bold.nii.gz
sub-02/ses-009/func/sub-02_ses-009_task-emotion_run-01_bold.nii.gz
sub-02/ses-009/func/sub-02_ses-009_task-motor_run-01_bold.nii.gz
sub-02/ses-009/func/sub-02_ses-009_task-relational_run-01_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-gambling_run-01_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-gambling_run-02_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-motor_run-01_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-social_run-01_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-social_run-02_bold.nii.gz
sub-02/ses-010/func/sub-02_ses-010_task-wm_run-02_bold.nii.gz
sub-03/ses-002/func/sub-03_ses-002_task-emotion_run-01_bold.nii.gz
sub-03/ses-002/func/sub-03_ses-002_task-motor_run-01_bold.nii.gz
sub-03/ses-002/func/sub-03_ses-002_task-relational_run-01_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-emotion_run-02_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-gambling_run-01_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-gambling_run-02_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-language_run-02_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-motor_run-01_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-motor_run-02_bold.nii.gz
sub-03/ses-003/func/sub-03_ses-003_task-relational_run-02_bold.nii.gz
sub-03/ses-004/func/sub-03_ses-004_task-emotion_run-01_bold.nii.gz
sub-03/ses-004/func/sub-03_ses-004_task-relational_run-01_bold.nii.gz
sub-03/ses-004/func/sub-03_ses-004_task-restingstate_run-01_bold.nii.gz
sub-03/ses-004/func/sub-03_ses-004_task-wm_run-01_bold.nii.gz
sub-03/ses-005/func/sub-03_ses-005_task-language_run-01_bold.nii.gz
sub-03/ses-005/func/sub-03_ses-005_task-relational_run-01_bold.nii.gz
sub-03/ses-005/func/sub-03_ses-005_task-restingstate_run-01_bold.nii.gz
sub-03/ses-006/func/sub-03_ses-006_task-gambling_run-02_bold.nii.gz
sub-03/ses-006/func/sub-03_ses-006_task-motor_run-01_bold.nii.gz
sub-03/ses-006/func/sub-03_ses-006_task-motor_run-02_bold.nii.gz
sub-03/ses-006/func/sub-03_ses-006_task-social_run-01_bold.nii.gz
sub-03/ses-007/func/sub-03_ses-007_task-emotion_run-01_bold.nii.gz
sub-03/ses-007/func/sub-03_ses-007_task-gambling_run-01_bold.nii.gz
sub-03/ses-007/func/sub-03_ses-007_task-language_run-01_bold.nii.gz
sub-03/ses-007/func/sub-03_ses-007_task-motor_run-01_bold.nii.gz
sub-03/ses-007/func/sub-03_ses-007_task-social_run-01_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-emotion_run-01_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-emotion_run-02_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-gambling_run-02_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-language_run-02_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-motor_run-01_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-motor_run-02_bold.nii.gz
sub-03/ses-008/func/sub-03_ses-008_task-relational_run-01_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-emotion_run-02_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-motor_run-01_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-relational_run-01_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-relational_run-02_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-social_run-02_bold.nii.gz
sub-03/ses-009/func/sub-03_ses-009_task-wm_run-01_bold.nii.gz
sub-05/ses-001/func/sub-05_ses-001_task-gambling_run-01_bold.nii.gz
sub-05/ses-001/func/sub-05_ses-001_task-relational_run-02_bold.nii.gz
sub-05/ses-001/func/sub-05_ses-001_task-social_run-02_bold.nii.gz
sub-05/ses-001/func/sub-05_ses-001_task-wm_run-01_bold.nii.gz
sub-05/ses-001/func/sub-05_ses-001_task-wm_run-02_bold.nii.gz
sub-05/ses-003/func/sub-05_ses-003_task-language_run-01_bold.nii.gz
sub-05/ses-003/func/sub-05_ses-003_task-social_run-01_bold.nii.gz
sub-05/ses-003/func/sub-05_ses-003_task-wm_run-01_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-gambling_run-01_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-gambling_run-02_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-language_run-01_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-language_run-02_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-motor_run-01_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-social_run-01_bold.nii.gz
sub-05/ses-004/func/sub-05_ses-004_task-social_run-02_bold.nii.gz
sub-05/ses-005/func/sub-05_ses-005_task-gambling_run-01_bold.nii.gz
sub-05/ses-005/func/sub-05_ses-005_task-motor_run-01_bold.nii.gz
sub-05/ses-005/func/sub-05_ses-005_task-relational_run-01_bold.nii.gz
sub-05/ses-005/func/sub-05_ses-005_task-social_run-01_bold.nii.gz
sub-05/ses-006/func/sub-05_ses-006_task-gambling_run-01_bold.nii.gz
sub-05/ses-006/func/sub-05_ses-006_task-restingstate_run-01_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-gambling_run-02_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-language_run-02_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-motor_run-02_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-relational_run-01_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-social_run-02_bold.nii.gz
sub-05/ses-008/func/sub-05_ses-008_task-wm_run-02_bold.nii.gz
sub-05/ses-009/func/sub-05_ses-009_task-motor_run-01_bold.nii.gz
sub-05/ses-009/func/sub-05_ses-009_task-social_run-01_bold.nii.gz
sub-05/ses-009/func/sub-05_ses-009_task-wm_run-01_bold.nii.gz
sub-05/ses-010/func/sub-05_ses-010_task-emotion_run-01_bold.nii.gz
sub-05/ses-010/func/sub-05_ses-010_task-gambling_run-01_bold.nii.gz
sub-05/ses-010/func/sub-05_ses-010_task-language_run-01_bold.nii.gz
sub-05/ses-010/func/sub-05_ses-010_task-relational_run-02_bold.nii.gz
```
