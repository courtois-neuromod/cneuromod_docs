# anat

This dataset contains anatomical sessions acquired longitudinally in the [CNeuroMod](https://cneuromod.ca) project (~2 sessions per year for 5 years, except `sub-05`).

:::{tip}
If you use this dataset, please cite:

Boudreau, M., Karakuzu, A., Boré, A., Pinsard, B., Zelenkovski, K., Alonso-Ortiz, E., Boyle, J., Bellec, L., & Cohen-Adad, J. (2025). _Longitudinal reproducibility of brain and spinal cord quantitative MRI biomarkers_. **Imaging Neuroscience** (Cambridge, Mass.), 3. [doi: 10.1162/imag_a_00409](https://doi.org/10.1162/imag_a_00409)
:::


✅ = available  ⬜ = collected but not yet integrated  ❌ = not collected

| Field       |  Description |
|-------------|--------------|
| Subjects    |  `sub-01` ✅ · `sub-02` ✅ · `sub-03` ✅ · `sub-04` ✅ · `sub-05` ✅ · `sub-06` ✅,|
| Duration    |  5-15 sessions with structural MRI per participant |
| Data        |  T1-weighted brain ✅ and spine ✅ |
|             |  T2-weighted brain ✅ and spine ✅ |
|             |  Diffusion-weighted brain ✅ and spine ✅ |
|             |  Magnetization Transfer brain ✅ and spine ✅|
|             |  Proton Density brain ✅ and spine ✅ |
|             |  Susceptibility-Weighted imaging brain ✅ |
|             |  Multi-echo GRE spinal cord ✅ |
| Resources   | 🔣 [Access the data on CONP](https://portal.conp.ca/dataset?id=projects/cneuromod) |
|             | 🔣 [Data versioning on GitHub](https://github.com/courtois-neuromod/anat) |
|             | 📖 [Docs](https://docs.cneuromod.ca/en/latest/DATASETS.html#hcptrt) |
|             | 📖 [Data Paper](https://doi.org/10.1162/imag_a_00409) |

## Contributors ✨
[Lune Bellec](http://github.com/lunebellec) 🎨 📖 🤔 · [Julie Boyle](https://github.com/julieaboyle1) 🔣 📆 🤔 🎨 · [Arnaud Bore](https://github.com/arnaudbore) 💻 🔣 · [Amal Boukhdhir](https://github.com/bamal) 🔣 · [Julien Cohen-Adad](http://www.neuro.polymtl.ca) 🎨 🤔 🔣 · [Emilie dessureault](https://github.com/emilie-dessureault) 🔣 📆 🤔 🎨 · [François Paugam](https://github.com/FrancoisPgm) 🔣 · [Marie-Ève Picard](https://github.com/me-pic) 🔣 ·  [Basile Pinsard](https://github.com/bpinsard) 🤔 🎨 📖 🔣 👀 🚧 💻 · [François Lespinasse](https://github.com/sangfrois) 🔣 · [Pravish Sainath](https://github.com/pravishsainath) 🔣 · Courtois Foundation 💰

Legend: 🎨 design · 📖 documentation · 🔣 data · 👀 review · 🚧 maintenance · 💻 code · 📆 project management · 🤔 ideas · 💬 questions · 🧑‍🏫 mentoring · 🐛 bug reports · 📓 user testing · 💰 funding

## Protocol
The anatomical dataset includes longitudinal anatomical images of the brain and upper spinal cord at an approximate rate of 4 sessions a year. The primary intended use of this dataset is to monitor the structural stability of the brain and spine of participants for the duration of the study. Many quantitative measures of brain structure can also be derived and included in analyses, such as gray matter morphometry, tractography or measures of myelination. Cortical flat maps cut with TkSurfer 6.0.0 are provided with the freesurfer derivatives for visualization.

The MRI sequences are described in more detailed in [](Brain_anatomical_sequences) and [](Spinal_cord_anatomical_sequences), including pdfs of the Siemens exam cards. Brain T1w, T2w and DWI were copied from the HCP aging and development protocol for Prisma MRI scanner.
Other sequences were selected and optimized by the Courtois NeuroMod team.

All images covering the face were anonymized by zeroing the data in the face, teeth and ears regions with a custom mask warped from the MNI space based on a linear registration of the T1w brain MRI series. This defacing script is available [here](https://github.com/courtois-neuromod/ds_prep/blob/main/mri/prepare/deface_anat.py)
