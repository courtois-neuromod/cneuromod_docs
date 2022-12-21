# MRI

## Image acquisition

### Scanner
<img src="./_static/mri/mri.jpg" alt="UNF MRI" width="350" align="right" hspace="10"/> Magnetic resonance imaging (MRI) for the Courtois neuromod project is being acquired at the functional neuroimaging unit ([UNF](https://unf-montreal.ca/)), located at the "Centre de Recherche de l'Institut Universitaire de Gériatrie de Montréal" ([CRIUGM](http://www.criugm.qc.ca/)) and affiliated with [University of Montreal](https://www.umontreal.ca/) as well as the [CIUSSS du Centre-Sud-de-l'île-de-Montréal](https://ciusss-centresudmtl.gouv.qc.ca/propos/services-en-anglais). The scanner is a Siemens Prisma Fit, equipped with a 2-channel transmit body coil and a 64-channel receive head/neck coil. Most imaging in the Courtois Neuromod project are composed solely of functional MRI runs. Periodically, an entire session is dedicated to anatomical scans.

### Personalized head cases
<img src="./_static/mri/headcase.png" alt="head case" width="200" align="right" hspace="10"/> In order to minimize movement, each participant wears a custom-designed, personalized headcase during scanning, built by [Caseforge](https://caseforge.co). The headcases are milled based on a head scan of each participant generated using a handheld 3D scanner, and the shape of the MRI coil. Caseforge mills the personalized headcases in polystyrene foam blocks.

## Sequences

### Functional sequences

The parameters of the functional MRI sequence relevant for data analysis can be found in the NeuroMod DataLad. The functional acquisition parameters are all identical to the one used in the `hcptrt` dataset. The Siemens exam card can be found [here](./_static/mri/functional_protocol_HCP-trt.pdf), and is briefly recapitulated below. Functional MRI data was acquired using an accelerated simultaneous multi-slice, gradient echo-planar imaging sequence [(Xu et al., 2013)](http://www.ncbi.nlm.nih.gov/pubmed/23899722) developed at the Center for Magnetic Resonance Research (CMRR) University of Minnesota, as part of the Human Connectome Project [(Glasser et al., 2016)](https://www.nature.com/articles/nn.4361). The sequence is available on the Siemens PRISMA scanner at UNF through a concept to production (C2P) agreement, and was used with the following parameters: slice acceleration factor = 4, TR = 1.49 s, TE = 37 ms, flip angle = 52 degrees, voxel size = 2 mm x 2 mm x 2 mm, 60 slices, acquisition matrix 96x96. In each session, a short acquisition (3 volumes) with reversed phase encoding direction was run to allow retrospective correction of B0 field inhomogeneity-induced distortion.

(Brain_anatomical_sequences)=
### Brain anatomical sequences

 The parameters of the brain anatomical MRI sequences relevant for data analysis can be found in the NeuroMod DataLad. The acquisition parameters are identical for all anatomical sessions. The Siemens pdf exam card of the anatomical sessions can be found [here](./_static/mri/anatomical_protocol_2019-01-22.pdf), and is briefly recapitulated below. A standard (brain) anatomical session started with a 21 s localizer scan, and then included the following sequences:
  * T1-weighted MPRAGE 3D sagittal sequence (duration 6:38 min, TR = 2.4 s, TE = 2.2 ms, flip angle = 8 deg, voxel size = 0.8 mm isotropic, R=2 acceleration)
  * T2-weighted FSE (SPACE) 3D sagittal sequence (duration 5:57 min, TR = 3.2 s, TE = 563 ms, voxel size = 0.8 mm isotropic, R=2 acceleration)
  * Diffusion-weighted 2D axial sequence (duration 4:04 min, TR = 2.3 s, TE = 82 ms, 57 slices, flip angle = 78 deg, voxel size = 2 mm isotropic,  phase-encoding P-A, SMS=3 through-plane acceleration, b-max = 3000 s/mm2). The same sequence was run with phase-encoding A-P to correct for susceptibility distortions.
  * gradient-echo magnetization-transfer 3D sequence (duration 3:34 min, 28 = ms, TE = 3.3 ms, flip angle = 6 deg, voxel size = 1.5 mm isotropic, R=2 in-plane GRAPPA, MT pulse Gaussian shape centered at 1.2 kHz offset).
  * gradient-echo proton density 3D sequence (same parameters as above, without the MT pulse).
  * gradient-echo T1-weighted 3D sequence (same parameters as above, except: TR = 18 ms, flip angle = 20 deg).
  * MP2RAGE 3D sequence (duration 7:26 min, TR = 4 s, TE = 1.51 ms, TI1 = 700 ms, TI2 = 1500 ms, flip angle 1 = 7 deg, flip angle 2 = 5 deg, voxel size = 1.2 mm isotropic, R=2 acceleration)
  * Susceptibility-weighted 3D sequence (duration 4:54 min, TR = 27 ms, TE = 20 ms, flip angle = 15 deg)

.. warning::  T1w, T2w and DWI (from HCP development/aging protocol for Siemens Prisma) and SWI do not have gradient non-linearity correction applied on the scanner. Offline correction can be applied using tools such as [gradunwarp](https://github.com/Washington-University/gradunwarp), but is not included yet in fMRIPrep pipeline.

(Spinal_cord_anatomical_sequences)=
### Spinal cord anatomical sequences

The parameters of the spinal cord anatomical MRI sequences relevant for data analysis can be found in the BIDS dataset, and included metadata. The acquisition parameters are identical for all anatomical sessions, and follow a community [spinal cord standard imaging protocol](https://osf.io/tt4z9/). The Siemens pdf exam card of the anatomical sessions can be found [here](./_static/mri/spine_generic_Prisma_VE11C_ZOOMit.pdf), and is briefly recapitulated below. A standard (spinal cord) anatomical session starts with a 21 s localizer scan, and then includes the following sequences:
 * T1-weighted 3D sagittal sequence (duration 4:44 min, TR = 2 s, TE = 3.72 ms, flip angle = 9 deg, voxel size = 1.0 mm isotropic, R=2 acceleration)
 * T2-weighted  3D sagittal sequence (duration 4:02 min, TR = 1.5 s, TE = 120 ms, flip angle = 120 deg, voxel size = 0.8 mm isotropic, R=3 acceleration)
 * Diffusion-weighted 2D axial sequence (cardiac-gated with pulseOx, approximate duration 3 min, TR = 620 ms, TE = 60 ms, voxel size = 0.9 x 0.9 x 0.5 mm, phase-encoding A-P, b-max = 800 s/mm2)
 * Gradient-echo magnetization-transfer 3D axial sequence (duration 2:12 min, TR = 35 ms, TE = 3.13 ms, flip angle = 9 deg, voxel size = 0.9 x 0.9 x 0.5 mm, R=2 acceleration, with MT Gaussian pulse)
 * Gradient-echo proton-density weighted 3D axial sequence (same parameters as above, without the MT pulse).
 * Gradient-echo T1-weighted 3D axial sequence (same parameters as above, except: TR = 15 ms, flip angle = 15 deg).
 * gradient-echo ME (duration 4:45 min, TR = 600 ms, effective TE = 14 ms (this is a multi-echo sequence), flip angle = 30 deg, voxel size = 0.9 x 0.9 x 0.5 mm, R=2 acceleration)

## Stimuli

### Visual presentation

All visual stimuli were projected using a Epson Powerlite L615U projector. The images were casted through a waveguide onto a blank screen located in the MRI room.

### Auditory system

For functional sessions, participant wore MRI compatible  S15 [Sensimetric](http://www.sens.com/products/model-s15/) headphone inserts, proving high-quality acoustic stimulation and substantial attenuation of background noise.  On the computer used for stimuli presentation, a custom impulse response of the headphones is applied with an online finite impulse response filter using the LADSPA DSP to all the presented stimuli.This impulse response was provided by the manufacturer. Sounds was amplified using an [AudioSource](http://audiosource.net/shop/amp100vs/) AMP100V amplifier, situated in the control room. Participants also wear earmuffs, adapted from commercially available [model](https://www.homedepot.ca/product/workhorse-foldable-head-band-earmuff-nrr-25/1001105366). The commercial earmuffs have been cut and glued back together in order to be thin enough to be used with the 64-channels MRI coil.

### Stimuli presentation

For the HCP-trt dataset, Eprime scripts provided by the Human Connectome project were adapted for our presentation system, and run using Eprime 2.0. For all other tasks, a custom overlay on top of the [psychopy library](https://www.psychopy.org/) was used to present the different tasks and synchronize task with the scanner trigger pulses.
This software also allowed to trigger the start of the eyetracking system, and onset the stimuli presentation. Trigger pulses were also recorded in the [AcqKnowledge software](https://www.biopac.com/product/acqknowledge-software/). All task stimuli scripts are available through [github](https://github.com/courtois-neuromod/task_stimuli).

## Physiological measures

### Biopac
During all sequences, electrophysiological signals were recorded using a Biopac M160  MRI compatible systems and amplifiers. Measurements were acquired at 1000 Hz. Recodings were synchronized to the MRI scans via trigger pulses. All measurements were recorded and monitored using Biopac's AcqKnowledge sofware.

### Plethysmograph
Participant cardiac pulse was measured using an MRI compatible plethysmograph. A Biopac TSD200-MRI photoplethysmogram transducer was  placed on the foot or toe of the participants to obtain beat-by-beat estimates of heart rate.

### Skin conductance
Skin conductance, was measured using two electrodes, one applied to the sole of the foot and the other to the ankle, to record the participant electrodermal response.

### Electrocardiogram
An electrocardiogram (ECG) was used to  measure the electrical activity generated by the heart. The ECG was recorded using three MRI compatible electrodes that were placed adjacent to one aother, on the lower left rib cage, just under the heart.

### Respiration
Participant’s respiration was measured using a custom MRI compatible respiration belt.  The respiration system consisted of: a pressure cuff taken from a blood pressure monitor (PhysioLogic blood), a pressure sensor (MPXV5004GC7U, NXP USA Inc), and flexible tubing. The cuff was attached to the participant upper abdomen using Velcro strap, and then connected to the pressure sensor, located outside the scanner room, using tubing passed through a waveguide. The pressure signal was recorded using an analog input on the Biopac system, and monitored using AcqKnowledge software.

## Mock scanner
Some of our datasets required a comparison between genuine in-scanner conditions and "mock" conditions, where the subject was installed in a fake scanner that reproduced the comfort and aspect of an MRI scanner. This mock setup was also located at [UNF](https://unf-montreal.ca/), and was equipped with a monitor screen for stimulus presentation as well as audio headphones and response devices (keyboard and video game controller).
