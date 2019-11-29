# Access

## Ethics

The Courtois NeuroMod project has been approved by the institutional research ethics board of the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The CIUSSS is a large governmental health organization, and the core NeuroMod team is based at the Research Centre of the Montreal Geriatric Institute ([CRIUGM](http://www.criugm.qc.ca/en.html)), which is a part of the CIUSSS, and affiliated with the [University of Montreal](https://www.umontreal.ca/). The ethics documentation may be useful for research teams to receive ethics approval for secondary analysis by their local institutions, if required.
  * [approval_irb_ciusss_french.pdf](./_static/ethics/approval_irb_ciusss_french.pdf): letter of approval from the institutional review board for the Courtois NeuroMod project (in French).
  * [courtois_neuromod_project_description.pdf](./_static/ethics/courtois_neuromod_project_description.pdf): scientific overview of the Courtois NeuroMod project (in English).
  * [consent_form_english.pdf](./_static/ethics/consent_form_english.pdf): the informed consent form signed by participants (English version).
  * [consent_form_french.pdf](./_static/ethics/consent_form_french.pdf): the informed consent form signed by participants (French version).

## Downloading the dataset

All data are made available as a [DataLad collection (login required)](https://git.unf-montreal.ca/cneuromod/cneuromod) in the [UNF git](https://git.unf-montreal.ca). [DataLad](https://www.datalad.org/) is a tool for versioning a large data structure in a git repository. The dataset can be explored without downloading the data, and it is easy to only download the subset of the data you need for your project.
See the [DataLad handbook](http://handbook.datalad.org/en/latest/) for further information.

To obtain the data, you need to install a recent version of the [DataLad software](http://handbook.datalad.org/en/latest/intro/installation.html), available for Linux, OSX and Windows. Note that you need to have valid login credentials to access the NeuroMod git as well as the NeuroMod [Amazon S3](https://aws.amazon.com/s3) fileserver. Once you have obtained these credentials, you can proceed as follows in a terminal:
```
# Install recursively the dataset and subdataset of the current project.
# If using ssh git clone as follow, you can set your public SSH key in the present git to ease future updates.
datalad install -r git@git.unf-montreal.ca:cneuromod/cneuromod.git
# If errors show up relative to .heudiconv subdataset/submodule, this is OK, they are not published (will be cleaned up in the future).
cd cneuromod

# You will most likely want to checkout a stable release tag for your analysis.
# You can do this while creating a new branch with the name you like.s
# In this branch you can run you analysis and commit your work.
# For instance (but this tag doesn't exist yet):
git checkout -b <myanalysisbranch> cneuromod-2020

# We now set as environment variable the credentials to the file server.
# The s3 access_key and secret_key will be provided upon request by the data manager.
# This needs to be set in your `bash` everytime you want to download data.
export AWS_ACCESS_KEY_ID=<s3_access_key>  AWS_SECRET_ACCESS_KEY=<s3_secret_key>

# Now you can get data using:
datalad get -r <any/file/in/the/dataset.example>

# You can also run reproductible analysis using
datalad run -i <the files needed for my analysis> ../path/to/my/analysis.script
# which will download the required files and store the command launched and the results in the datalad dataset.

```

## Updates

The dataset will be updated with new releases so you might want to get these changes (unless you are running analyses, or trying to reproduce results). The master branch will evolve with the project, and can be unstable or messy.
Thus, we recommend using specific release tags. There is one stable release per year, e.g. `cneuromod-2020`, which is preceded by alpha (e.g. `cneuromod-2020-alpha`), beta (e.g. `cneuromod-2020-beta`) and release candidate (e.g. `cneuromod-2020-rc`). To update your dataset to the latest version, use:

```
# update the dataset recursively
datalad update -r --merge

```
Once your local dataset clone is updated, you might need to pull new data, as some files could have been replace.
