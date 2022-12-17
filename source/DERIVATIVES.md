# Derivatives

## [sMRIPrep](https://github.com/courtois-neuromod/anat.smriprep)

The anatomical data was preprocessed using [sMRIPrep pipeline](https://github.com/nipreps/smriprep).
It took as input the T1w and T2w of the first 2 sessions of all participants, which were averaged after coregistration.

## [fMRIPrep](https://github.com/courtois-neuromod/cneuromod.fmriprep)

### Overview
The functional data was preprocessed using the [fMRIprep pipeline](https://fmriprep.readthedocs.io/en/stable/installation.html). FmriPrep is an fMRI data preprocessing pipeline that requires minimal user input, while providing error and output reporting. It performs basic processing steps (coregistration, normalization, unwarping, noise component extraction, segmentation, skullstripping etc.) and provides outputs that can be easily submitted to a variety of group level analyses, including task-based or resting-state fMRI, graph theory measures, surface or volume-based statistics, etc. The fMRIprep pipeline uses a combination of tools from well-known software packages, including FSL, ANTs, FreeSurfer and [AFNI](https://afni.nimh.nih.gov/). For additional information regarding fMRIPrep installation, workflow and outputs, please visit the [documentation page](https://fmriprep.readthedocs.io/en/stable/installation.html).
Note that the `slicetiming` option was disabled (i.e. fMRIprep was invoked with the flag `--ignore slicetiming`).

### Outputs
The outputs of fMRIprep can be found as sub-datasets of the [cneuromod.processed](https://github.com/courtois-neuromod/cneuromod.processed) super-dataset.
fMRIPrep functional preprocessing was run using the anatomical "fast-track" (flag `--anat-derivatives`) with sMRIPrep output described above, so as to use the same anatomical basis for all functional dataset.
The output was generated in `T1w`, `MNI152NLin2009cAsym` and `fsLR-den-91k` spaces as defined by [templateflow](https://www.templateflow.org/) to respectively enable native space and volumetric or surface-based analyses.

The description of participant, session, task and event tags can be found in the [Datasets](DATASETS.html) section. Each participant folder (`sub-*`) contains:
- `ses-*/func` containing for each fMRI run of that session file prefixed with:
  - `*_boldref.nii.gz` : a BOLD single volume reference.
  - `*_desc-brain_mask.nii.gz` : the brain mask in fMRI space.
  - `*_desc-preproc_bold.nii.gz` : the preprocessed BOLD timeseries.
  - `*_desc-confounds_timeseries.tsv` : a tabular tsv file, containing a large set of confounds to use in analysis steps (eg. GLM).

### Recommended preprocessing strategy
The confounding regressors are correlated, thus it is critical to only use a subset of these regressors. Also note that preprocessed time series have not been corrected for any confounds, but simply realigned in space, and it is therefore also critical to regress some of the available confounds prior to analysis. See the [fMRIprep documentation](https://fmriprep.org/en/stable/outputs.html#confounds) for details on available confound regressors. For python users, we recommend using [nilearn](https://nilearn.github.io) and the tool [load_confounds_strategy](https://nilearn.github.io/stable/modules/generated/nilearn.interfaces.fmriprep.load_confounds_strategy.html) to load confounds from the fMRIprep outputs, using with a standardized strategy. As the NeuroMod data consistently exhibits low levels of motion, we recommend against removing time points with excessive motion (aka scrubbing), and the `minimal` strategy available in nilearn is a reasonable choice. Because of the 2 mm spatial resolution of the fMRI scan, there is substantial impact of thermal noise, and some amount of spatial smoothing is advisable, the extent of it being determined by your hypotheses and analysis.

### Pipeline description

Results included in this manuscript come from preprocessing
performed using *fMRIPrep* 20.2.5
(@fmriprep1; @fmriprep2; RRID:SCR_016216),
which is based on *Nipype* 1.6.1
(@nipype1; @nipype2; RRID:SCR_002502).

Anatomical data preprocessing

: A total of 0 T1-weighted (T1w) images were found within the input
BIDS dataset.
Anatomical preprocessing was reused from previously existing derivative objects.


Functional data preprocessing

: For each of the 2 BOLD runs found per subject (across all
tasks and sessions), the following preprocessing was performed.
First, a reference volume and its skull-stripped version were generated
by aligning and averaging
1 single-band references (SBRefs).
A B0-nonuniformity map (or *fieldmap*) was estimated based on two (or more)
echo-planar imaging (EPI) references with opposing phase-encoding
directions, with `3dQwarp` @afni (AFNI 20160207).
Based on the estimated susceptibility distortion, a corrected
EPI (echo-planar imaging) reference was calculated for a more
accurate co-registration with the anatomical reference.
The BOLD reference was then co-registered to the T1w reference using
`bbregister` (FreeSurfer) which implements boundary-based registration [@bbr].
Co-registration was configured with six degrees of freedom.
Head-motion parameters with respect to the BOLD reference
(transformation matrices, and six corresponding rotation and translation
parameters) are estimated before any spatiotemporal filtering using
`mcflirt` [FSL 5.0.9, @mcflirt].
First, a reference volume and its skull-stripped version were generated
 using a custom
methodology of *fMRIPrep*.
The BOLD time-series were resampled onto the following surfaces
(FreeSurfer reconstruction nomenclature):
*fsaverage*.
The BOLD time-series (including slice-timing correction when applied)
were resampled onto their original, native space by applying
a single, composite transform to correct for head-motion and
susceptibility distortions.
These resampled BOLD time-series will be referred to as *preprocessed
BOLD in original space*, or just *preprocessed BOLD*.
The BOLD time-series were resampled into standard space,
generating a *preprocessed BOLD run in MNI152NLin2009cAsym space*.
First, a reference volume and its skull-stripped version were generated
 using a custom
methodology of *fMRIPrep*.
*Grayordinates* files [@hcppipelines] containing 91k samples were also
generated using the highest-resolution ``fsaverage`` as intermediate standardized
surface space.
Several confounding time-series were calculated based on the
*preprocessed BOLD*: framewise displacement (FD), DVARS and
three region-wise global signals.
FD was computed using two formulations following Power (absolute sum of
relative motions, @power_fd_dvars) and Jenkinson (relative root mean square
displacement between affines, @mcflirt).
FD and DVARS are calculated for each functional run, both using their
implementations in *Nipype* [following the definitions by @power_fd_dvars].
The three global signals are extracted within the CSF, the WM, and
the whole-brain masks.
Additionally, a set of physiological regressors were extracted to
allow for component-based noise correction [*CompCor*, @compcor].
Principal components are estimated after high-pass filtering the
*preprocessed BOLD* time-series (using a discrete cosine filter with
128s cut-off) for the two *CompCor* variants: temporal (tCompCor)
and anatomical (aCompCor).
tCompCor components are then calculated from the top 2% variable
voxels within the brain mask.
For aCompCor, three probabilistic masks (CSF, WM and combined CSF+WM)
are generated in anatomical space.
The implementation differs from that of Behzadi et al. in that instead
of eroding the masks by 2 pixels on BOLD space, the aCompCor masks are
subtracted a mask of pixels that likely contain a volume fraction of GM.
This mask is obtained by dilating a GM mask extracted from the FreeSurfer's *aseg* segmentation, and it ensures components are not extracted
from voxels containing a minimal fraction of GM.
Finally, these masks are resampled into BOLD space and binarized by
thresholding at 0.99 (as in the original implementation).
Components are also calculated separately within the WM and CSF masks.
For each CompCor decomposition, the *k* components with the largest singular
values are retained, such that the retained components' time series are
sufficient to explain 50 percent of variance across the nuisance mask (CSF,
WM, combined, or temporal). The remaining components are dropped from
consideration.
The head-motion estimates calculated in the correction step were also
placed within the corresponding confounds file.
The confound time series derived from head motion estimates and global
signals were expanded with the inclusion of temporal derivatives and
quadratic terms for each [@confounds_satterthwaite_2013].
Frames that exceeded a threshold of 0.5 mm FD or
1.5 standardised DVARS were annotated as motion outliers.
All resamplings can be performed with *a single interpolation
step* by composing all the pertinent transformations (i.e. head-motion
transform matrices, susceptibility distortion correction when available,
and co-registrations to anatomical and output spaces).
Gridded (volumetric) resamplings were performed using `antsApplyTransforms` (ANTs),
configured with Lanczos interpolation to minimize the smoothing
effects of other kernels [@lanczos].
Non-gridded (surface) resamplings were performed using `mri_vol2surf`
(FreeSurfer).


Many internal operations of *fMRIPrep* use
*Nilearn* 0.6.2 [@nilearn, RRID:SCR_001362],
mostly within the functional processing workflow.
For more details of the pipeline, see [the section corresponding
to workflows in *fMRIPrep*'s documentation](https://fmriprep.readthedocs.io/en/latest/workflows.html "FMRIPrep's documentation").


### Copyright Waiver

The above boilerplate text was automatically generated by fMRIPrep
with the express intention that users should copy and paste this
text into their manuscripts *unchanged*.
It is released under the [CC0](https://creativecommons.org/publicdomain/zero/1.0/) license.
