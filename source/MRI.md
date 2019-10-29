# MRI

Magnetic resonance imaging (MRI) for the Courtois neuromod project is being acquired at the functional neuroimaging unit ([UNF](https://unf-montreal.ca/)), located at the "Centre de Recherche de l'Institut Universitaire de Gériatrie de Montréal" ([CRIUGM](http://www.criugm.qc.ca/)) and affiliated with [Université de Montréal](https://www.umontreal.ca/) as well as the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The scanner is a Siemens Prisma Fit, with a 64 channels head coil. Most imaging in the Courtois Neuromod project are composed solely of functional MRI runs. Periodically, an entire session is dedicated to anatomical scans. The scanning environment includes a number of stimulation and response equipment, detailed below.   

## Personalized head cases
<img src="./_static/mri/headcase.png" alt="head case" width="200" align="right" hspace="10"/> In order to minimize movement during neuroimaging scans, each participant wears a custom-designed, personalized headcase built by a company called [Caseforge](https://caseforge.co) during scanning. The headcase are milled based on a scan of each participant's head generated using a handheld 3D scanner, as well as the shape of the MRI coil. Caseforge  mills the personalized headcases in foam blocks.

## Stimuli

### Visual presentation

All visual stimuli were presented with a projector onto a blank screen located in the MRI room, through a waveguide.

### Auditory system

For functional sessions, participant are equipped with MRI compatible headphone inserts.
On the computer used for stimuli presentation, a custom impulse response of the headphones is applied with an online finite impulse response filter using the LADSPA DSP to all the presented stimuli.
This impulse response was provided by the manufacturer.

### HCPTRT Stimuli

Eprime scripts provided by the Human Connectome project were adapted for our presentation system and used in the study

### Other stimuli

A custom overlay on top of Psychopy was used to present the different tasks and synchronize task with the scanner TTL.

## Video  game controller

## Functional acquisitions

TODO: acq params

For further information regarding the fMRI data structure and parameters, consult the BIDS dataset and included metadata.
[BIDS dataset](https://git.unf-montreal.ca/neuromod/)

## Anatomical acquisitions

### Brain


Localizer:          ~0:21
ANA T1W:             6:38
ANA T2W:             5:57
DWI:                 4:04
GRE3D_MTW    :       3:34
GRE3D_PDW    :       3:34
GRE3D_T1W    :       2:18
TFL_b1MAP_6MM:       0:21
T1_MPRAGE:           7:26
T2_SWI_TRA_P2_!5MM:  4:54


### Cervical spinal cord

A detailed description of the protocol can be found here: [Spinal Cord MRI Protocols](https://osf.io/tt4z9/), including sequences ported to other MRI manufacturers.

Localizer:         ~0:21
T2W:                4:02
*DWI gated:        ~2:12  
GRE_MTI:            2:12
GRE_MTO:            2:12
GRE_T1W:            0:57
GRE_ME:             4:45


TODO: acq params, link to osf.io of JCA protocol
