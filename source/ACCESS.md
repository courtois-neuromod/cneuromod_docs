# Access

## Ethics

The Courtois NeuroMod project has been approved by the institutional research ethics board of the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The CIUSSS is a large governmental health organization, and the core NeuroMod team is based at the Research Centre of the Montreal Geriatric Institute ([CRIUGM](http://www.criugm.qc.ca/en.html)), which is a part of the CIUSSS, and affiliated with the [Université de Montréal](https://www.umontreal.ca/). The ethics documentation may be useful for research teams to receive ethics approval for secondary analysis by their local institutions, if required.
  * [approval_irb_ciusss_french.pdf](./_static/ethics/approval_irb_ciusss_french.pdf): letter of approval from the institutional review board for the Courtois NeuroMod project (in French).
  * [courtois_neuromod_project_description.pdf](./_static/ethics/courtois_neuromod_project_description.pdf): scientific overview of the Courtois NeuroMod project (in English).
  * [consent_form_english.pdf](./_static/ethics/consent_form_english.pdf): the informed consent form signed by participants (English version).
  * [consent_form_french.pdf](./_static/ethics/consent_form_french.pdf): the informed consent form signed by participants (French version).

## Downloading the dataset

This is a [datalad](https://www.datalad.org/) dataset.
Quickly: datalad is a tool for versioning large data structure in a git repository using git-annex. The dataset can be explored without downloading the data, and it is easy to only download the subset of the data you need for your project.

To obtain the data, you must install a recent version of the [datalad software](https://www.datalad.org/get_datalad.html). You will also need to have access to the git hosting the dataset structure and to the S3 fileserver hosting the data.

Once you have that you can proceed as follow

```
# install recursively the dataset and subdataset of the current project
# if using ssh git clone as follow, you can set your public SSH key in the present git to ease future updates.
datalad install -r git@git.unf-montreal.ca:cneuromod/cneuromod.git
# if errors show up relative to .heudiconv subdataset/submodule, this is OK, they are not published (will be cleaned up in the future).
cd cneuromod


# We now set as environment variable the credentials to the file server.
# the s3 access_key and secret_key will be provided upon request by the data manager.
# This needs to be set in your `bash` everytime you want to download data.
export AWS_ACCESS_KEY_ID=<s3_access_key>  AWS_SECRET_ACCESS_KEY=<s3_secret_key>

# now you can get data using
datalad get -r <any/file/in/the/dataset.example>

# You can also run reproductible analysis using
datalad run -i <the files needed for my analysis> ../path/to/my/analysis.script
# which will download the required files and store the command launched and the results in the datalad dataset.

```

### Dataset updates

The dataset will be updated with new data, new preprocessing pipelines, fixes... so you might want to get these changes (unless you are running analyses, or trying to reproduce results).
The master branch will evolve with the project, and can be unstable or messy.
Thus, we recommend using specific release tags, unless critical fixes are provided after the release and could unvalidate your analyses.

```
# update the dataset recursively
datalad update -r --merge

```

Once your local dataset clone is updated, you might need to pull new data, as some files could have been replace.
