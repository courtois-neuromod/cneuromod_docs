# Access to Data

## Partial fully unrestricted data access

Four CNeuroMod subjects (`sub-01`, `sub-02`, `sub-03` and `sub-05`) have chosen to openly share their data via the Canadian Open Neuroscience Platform ([CONP]([https://portal.conp.ca/](https://portal.conp.ca/dataset?id=projects/cneuromod))). These data are distributed under a liberal Creative Commons data license, in particular authorizing re-share of derivates. Note that you can use the instructions in this guide directly - the command will retrieve all the CONP data and throw warnings about the other subjects, which require an access key to download (see next Section for full access). 

## Complete CNeuroMod databank via Data Transfer Agreement (DTA)

To access all the data available in the CNeuroMod databank (i.e all 6 subjects) researchers are required to complete a form with a brief description of planned analyses, and complete an inter-institutional data transfer agreement. Links to relevant forms can be found on the [access request page](https://www.cneuromod.ca/access/access/). The data transfer agreement must be signed by the researcher responsible for the project as well as a representative of the main academic institution where the research team is affiliated. The application will be evaluated by a data access committee and, if approved, a transfer key will be shared with the research team in order to transfer the data (see [Downloading the dataset](downloading) section below).


## Ethics

The Courtois NeuroMod project has been approved by the institutional research ethics board of the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The CIUSSS is a large governmental health organization, and the core NeuroMod team is based at the Research Centre of the Montreal Geriatric Institute ([CRIUGM](http://www.criugm.qc.ca/en.html)), which is a part of the CIUSSS, and affiliated with the [University of Montreal](https://www.umontreal.ca/). The consent forms signed by participants and the project description are available below. The formal authorization lettre from the ethics committee is available upon request. The project was  most recently renewed by the [Comité d’éthique de la recherche — Vieillissement et neuroimagerie (CER-VN)](https://ccsmtl-mission-universitaire.ca/fr/cer-vieillissement-et-neuroimagerie) on  October 21st, 2022 under the project number CER VN 18-19-22, and title "Extensive characterization of human brain activity under naturalistic stimulations for developing
individual artificial neuronal models."

  * [courtois_neuromod_project_description.pdf](./_static/ethics/courtois_neuromod_project_description.pdf): scientific overview of the Courtois NeuroMod project (in English).
  * [consent_form_english.pdf](./_static/ethics/consent_form_english.pdf): the informed consent form signed by participants (English version).
  * [consent_form_french.pdf](./_static/ethics/consent_form_french.pdf): the informed consent form signed by participants (French version).

(downloading)=
## Downloading the dataset
All data are made available as a [DataLad collection](https://github.com/courtois-neuromod/cneuromod) on github in public repositories.
[DataLad](https://www.datalad.org/) is a tool for versioning a large data structure in a git repository. The dataset can be explored without downloading the data, and it is easy to only download the subset of the data you need for your project.
See the [DataLad handbook](http://handbook.datalad.org/en/latest/) for further information.

We recommend creating an SSH key (if not already present) on the machine on which the dataset will be installed and adding it to github. See the official [github instructions](https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account) on how to create and add a key to your account.

To obtain the data, you need to install a recent version of the [DataLad software](http://handbook.datalad.org/en/latest/intro/installation.html), available for Linux, OSX and Windows. Note that you need to have valid login credentials to access the NeuroMod git as well as the NeuroMod [Amazon S3](https://aws.amazon.com/s3) fileserver. Once you have obtained these credentials, you can proceed as follows in a terminal:
```
# Install recursively the dataset and subdataset of the current project.
# If using ssh git clone as follow, you can set your public SSH key in the present git to ease future updates.
datalad install -r git@github.com:courtois-neuromod/cneuromod.git
# If errors show up relative to .heudiconv subdataset/submodule, this is OK, they are not published (will be cleaned up in the future).
cd cneuromod
```

### Versioning

By default, this will install the latest stable release of the dataset, which is the recommended version to get for a new analysis.
If you are need to work on a specific version (for instance to reproduce a result), you can change to the appropriate tag with.
```
git checkout 2020
```

We now set as environment variable the credentials to the file server. The s3 access_key and secret_key will be provided by the data manager after being granted access to cneuromod by the user access committee.
```
# This needs to be set in your `bash` everytime you want to download data.
export AWS_ACCESS_KEY_ID=<s3_access_key>  AWS_SECRET_ACCESS_KEY=<s3_secret_key>
```

### Preprocessed data

For analysis of fMRI data, it is preferable to directly get the preprocessed data (smriprep and fmriprep for now).

```
datalad install git@github.com:courtois-neuromod/cneuromod.processed.git
cd cneuromod.processed
```

You can install the sub-datasets you are interested in (instead of installing all of them) using for instance:
```
datalad get -n smriprep fmriprep/movie10
```
and then get only the files you need (for instance MNI space output):
```
datalad get smriprep/sub-*/anat/*space-MNI152NLin2009cAsym_* # get all anatomical output in MNI space
datalad get fmriprep/movie10/sub-*/ses-*/func/*space-MNI152NLin2009cAsym_* # get all functional output in MNI space
```
You can add the flag `-J n` to download files in parallel with `n` being the number of threads to use.

The source data used for preprocessing (including raw data) are referenced as sources in the preprocessed dataset following [Yoda](https://handbook.datalad.org/en/latest/basics/101-127-yoda.html), so as to track provenance.
You can also track the version of the cneuromod dataset you are using by installing it in a datalad dataset created for your project.


### Stimuli and event files

You will likely need the events files and stimuli for your analysis which can be obtained from the sourcedata reference sub-datasets, for example:
```
datalad get -r fmriprep/movie10/sourcedata/movie10/stimuli fmriprep/movie10/sourcedata/movie10/*_events.tsv
```

or to get subject specific event files for tasks collecting behavioral responses:
```
datalad get -r fmriprep/movie10/sourcedata/hcptrt/sub-*/ses-*/func/*_events.tsv
```

## Updates

The dataset will be updated with new releases so you might want to get these changes (unless you are currently running analyses, or trying to reproduce results). The main branches of all datasets will always track the latest stable release.

```
# update the dataset recursively
datalad update -r --merge --reobtain-data

```
Once your local dataset clone is updated, you might need to pull new data, as some files could have been added or modified. The `--reobtain-data` flag should automatically pull files that you had already downloaded in case these were modified.
