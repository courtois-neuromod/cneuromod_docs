BIDS
====
All functional and anatomical data have been formatted in [BIDS](https://bids.neuroimaging.io/), for more information visit the Brain Imaging Data Structure documentation [site](https://bids-specification.readthedocs.io/en/stable/).
Some of the files do not follow the main BIDS convention:
- Anatomical sequences with multiple contrasts are following [BEP001](https://bids.neuroimaging.io/bep001).
- Spinal cord imaging use Body Part tag proposed in [BEP025](https://bids.neuroimaging.io/bep025) (`bp-cspine`) to allow to distinguish them from brain anatomical images acquired with the same contrasts.

Note that BIDS session names have no meaning apart from being data acquired in the same session. The number of runs, the tasks and their order within each session will not match from one participant to another. Note that a few session indices are skipped if the whole session was discarded for various scanning issues.

Participants
============

Six healthy participants (aged 31 to 47 at the time of recruitment in 2018), 3 women (`sub-03`, `sub-04` and `sub-06`) and 3 men (`sub-01`, `sub-02` and `sub-05`) consented to participate in the Courtois Neuromod Project for at least 5 years. Three of the participants reported being native francophone speakers (`sub-01`, `sub-02` and `sub-04`), one as being a native anglophone (`sub-06`) and two as bilingual native speakers (`sub-03` and `sub-05`).   All participants reported the right hand as being their dominant hand and reported being in good general health.

Exclusion criteria included visual or auditory impairments that would prevent participants from seeing and/or hearing stimuli in the scanner and major psychiatric or neurological problems. Standard exclusion criteria for MRI and MEG were also applied. Lastly, given that all stimuli and instructions are presented in English, all participants had to report having an advanced comprehension of the English language for inclusion.

Datasets
========

.. toctree::
   :maxdepth: 1
   :caption: Datasets

   hcptrt_bids
   anat
