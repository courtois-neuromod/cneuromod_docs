# Usage

We here describe how to use a subset of the cneuromod dataset with a common use case of fMRI analysis.

:::{important}
This use case if mostly for external user, as cneuromod team and students have more efficient ways to access the data on shared resources (HPC, local servers).
:::

The prerequisite is to have a recent working installation of datalad (including git and git-annex dependencies) and to have setup your SSH key on github.

## Recommended: create a datalad project

We highly recommend to run you analysis in a datalad dataset as to track provenance for reproducibility.

```
cd path/to/where/you/want/your/project/to/live
datalad create my_project_on_cneuromod
cd my_project_on_cneuromod
```

Alternative: just create a folder where to run your analysis, same number of lines/efforts, less advantages.

```
cd path/to/where/you/want/your/project/to/live
mkdir my_project_on_cneuromod
cd my_project_on_cneuromod
```

## Install the cneuromod processed datasets

For most users, the preprocessed data will conveniently save time.

Install the preprocessed super-dataset in your project:
```
datalad install -d ./ git@github.com:courtois-neuromod/cneuromod.processed.git
```
Your project now tracks which version of the dataset you are using.

If you are not following the recommended step above, run instead:
```
datalad install git@github.com:courtois-neuromod/cneuromod.processed.git
```

## Get the dataset(s) that you are interested in

Let say you want to get Movie10 data for your analysis, let's get the dataset.

```
datalad get -r -R2 -n ./cneuromod.processed/fmriprep/movie10
```
The `-r -R2` asks to recursively clone nested sub-datasets down to 2 levels below, most of the data of interest should be in that depth.
That command went relatively fast: only the structure of the dataset is pulled from github, the gigabytes of data are not downloaded yet.

You could repeat that single line for other sub-datasets if you want to combine multiple ones for your analysis.

You can now explore the structure of that dataset.


Lets have a look at what the preprocessed functional data looks like (truncated).
```
$ ls ./cneuromod.processed/fmriprep/movie10/sub-01/ses-001/func/
sub-01_ses-001_task-bourne01_desc-confounds_timeseries.json
sub-01_ses-001_task-bourne01_desc-confounds_timeseries.tsv
sub-01_ses-001_task-bourne01_from-scanner_to-T1w_mode-image_xfm.txt
sub-01_ses-001_task-bourne01_from-T1w_to-scanner_mode-image_xfm.txt
sub-01_ses-001_task-bourne01_space-fsLR_den-91k_bold.dtseries.json
sub-01_ses-001_task-bourne01_space-fsLR_den-91k_bold.dtseries.nii
sub-01_ses-001_task-bourne01_space-fsLR_den-91k_bold.json
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_boldref.nii.gz
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-aparcaseg_dseg.nii.gz
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-aseg_dseg.nii.gz
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-brain_mask.json
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-brain_mask.nii.gz
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-preproc_bold.json
sub-01_ses-001_task-bourne01_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz
sub-01_ses-001_task-bourne01_space-T1w_boldref.nii.gz
sub-01_ses-001_task-bourne01_space-T1w_desc-aparcaseg_dseg.nii.gz
sub-01_ses-001_task-bourne01_space-T1w_desc-aseg_dseg.nii.gz
sub-01_ses-001_task-bourne01_space-T1w_desc-brain_mask.json
sub-01_ses-001_task-bourne01_space-T1w_desc-brain_mask.nii.gz
sub-01_ses-001_task-bourne01_space-T1w_desc-preproc_bold.json
sub-01_ses-001_task-bourne01_space-T1w_desc-preproc_bold.nii.gz
.
.
.
```
For each fMRI run acquired in a session, we can see that data are output in different spaces.
- space-T1w the individual anatomy of the participant
- space-MNI152NLin2009cAsym the MNI volumetric template
- space-fsLR_den-91k a surface based template
Most likely, you will choose a specific space for your analysis based on your hypothesis.
```
export space=T1w
```

Lets continue to explore the dataset structure.
The preprocessed functional data were generated from different source data.
```
$ ls -1 ./cneuromod.processed/fmriprep/movie10/sourcedata
movie10 ## this is the raw BIDS data
smriprep ## the preprocessed anatomical data for registration, segmentation and masking
templateflow ## the templates from the templateflow packages
```
The main interesting thing the raw BIDS data contains are event files.
```
$ column -tn ./cneuromod.processed/fmriprep/movie10/sourcedata/movie10/task-figures01_events.tsv
onset  duration  stim_file
0      598.18    figures/figures01.mkv
```
In the case of movie watching, this is pretty simple, the movie starts at the first TR onset, and the stim_file is a single MKV file, which following BIDS standard is located in the stimuli folder.

```
$ ls -la ./cneuromod.processed/fmriprep/movie10/sourcedata/movie10/stimuli/figures/
cut_figures.sh  figures02.mkv  figures04.mkv  figures06.mkv  figures08.mkv  figures10.mkv  figures12.mkv
figures01.mkv   figures03.mkv  figures05.mkv  figures07.mkv  figures09.mkv  figures11.mkv
```

## Download data

To start downloading the preprocessed fMRI, it's better to only get what you really need to save storage space.
The prerequisite is to have the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY environment variables set with the provided credentials.
If you want all data in a certain space:
```
datalad get ./cneuromod.processed/fmriprep/movie10/sub-01/ses-001/func/*space-${space}*
```
Or if you are only interested in a specific task or tasks set (here movies figures and life):
```
datalad get ./cneuromod.processed/fmriprep/movie10/sub-01/ses-001/func/*task-{figures,life}*_space-${space}*
```

Same thing goes for the stimuli.
```
datalad get ./cneuromod.processed/fmriprep/movie10/sourcedata/movie10/stimuli/{figures,life}/
```


You might also need anatomical data
```
datalad get movie10.fmriprep/sourcedata/smriprep/sub-*/anat/
```

You should now be ready to run analysis on these data.
