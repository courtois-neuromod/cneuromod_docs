# Access

## Data Transfer Agreement (DTA)

To access the cneuromod dataset, it is required to complete a form with a brief description of planned analyses, and complete an inter-institutional data transfer agreement. Links to relevant forms can be found on the [access request page](https://www.cneuromod.ca/access/access/).The data transfer agreement must be signed by the researcher responsible for the project as well as a representative of the main academic institution where the research team is affiliated. The application will be evaluated by a data access committee and, if approved, a transfer key will be shared with the research team in order to transfer the data (see [Downloading the dataset](downloading) section below).


## Ethics

The Courtois NeuroMod project has been approved by the institutional research ethics board of the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The CIUSSS is a large governmental health organization, and the core NeuroMod team is based at the Research Centre of the Montreal Geriatric Institute ([CRIUGM](http://www.criugm.qc.ca/en.html)), which is a part of the CIUSSS, and affiliated with the [University of Montreal](https://www.umontreal.ca/). The consent forms signed by participants and the project description are available below. The formal authorization lettre from the ethics committee is available upon request.
  * [courtois_neuromod_project_description.pdf](./_static/ethics/courtois_neuromod_project_description.pdf): scientific overview of the Courtois NeuroMod project (in English).
  * [consent_form_english.pdf](./_static/ethics/consent_form_english.pdf): the informed consent form signed by participants (English version).
  * [consent_form_french.pdf](./_static/ethics/consent_form_french.pdf): the informed consent form signed by participants (French version).

(downloading)=
## Downloading the dataset
All data are made available as a [DataLad collection (currently requires to be part of the cneuromod team)](https://github.com/courtois-neuromod/cneuromod) on github.
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
You will most likely want to checkout a stable release tag for your analyses. For instance:
```
git checkout cneuromod-2020
```
We now set as environment variable the credentials to the file server. The s3 access_key and secret_key will be provided by the data manager after being granted access to cneuromod by the user access committee.
```
# This needs to be set in your `bash` everytime you want to download data.
export AWS_ACCESS_KEY_ID=<s3_access_key>  AWS_SECRET_ACCESS_KEY=<s3_secret_key>
```
You can now get data using:
```
datalad get -r <any/file/in/the/dataset.example>
```

## Updates

The dataset will be updated with new releases so you might want to get these changes (unless you are running analyses, or trying to reproduce results). The master branch will evolve with the project, and can be unstable or messy.
Thus, we recommend using specific release tags.

```
git checkout 2020-alpha2 # checkout the dataset tag
git submodule update --init # checkout the subdatasets corresponding commits
```

There is one stable release per year, e.g. `cneuromod-2020`, which is preceded by one or multiple alpha release (e.g. `cneuromod-2020-alpha`), beta release (e.g. `cneuromod-2020-beta`) and release candidate (e.g. `cneuromod-2020-rc`). To update your dataset to the latest version, use:

```
# update the dataset recursively
datalad update -r --merge

```
Once your local dataset clone is updated, you might need to pull new data, as some files could have been added or changed.
