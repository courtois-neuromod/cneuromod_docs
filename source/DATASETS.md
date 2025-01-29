# Datasets

## BIDS

All functional and anatomical data has been formatted in [BIDS](https://bids.neuroimaging.io/), for more information visit the Brain Imaging Data Structure documentation [site](https://bids-specification.readthedocs.io/en/stable/).
Some of the files do not follow the main BIDS convention:
- Anatomical sequences with multiple contrasts are following [BEP001](https://bids.neuroimaging.io/bep001).
- Spinal cord imaging use Body Part tag proposed in [BEP025](https://bids.neuroimaging.io/bep025) (`bp-cspine`) to allow to distinguish them from brain anatomical images acquired with the same contrasts.

Note that BIDS session names have no meaning apart from being data acquired in the same session. The number of runs, the tasks and their order within each session will not match from one participant to another. Note that a few session indices are skipped if the whole session was discarded for various scanning issues.

## Participants

Six healthy participants (aged 31 to 47 at the time of recruitment in 2018), 3 women (`sub-03`, `sub-04` and `sub-06`) and 3 men (`sub-01`, `sub-02` and `sub-05`) consented to participate in the Courtois Neuromod Project for at least 5 years. Three of the participants reported being native francophone speakers (`sub-01`, `sub-02` and `sub-04`), one as being a native anglophone (`sub-06`) and two as bilingual native speakers (`sub-03` and `sub-05`).   All participants reported the right hand as being their dominant hand and reported being in good general health.

Exclusion criteria included visual or auditory impairments that would prevent participants from seeing and/or hearing stimuli in the scanner and major psychiatric or neurological problems. Standard exclusion criteria for MRI and MEG were also applied. Lastly, given that all stimuli and instructions are presented in English, all participants had to report having an advanced comprehension of the English language for inclusion.

## anat

The anatomical dataset includes longitudinal anatomical images of the brain and upper spinal cord at an approximate rate of 4 sessions a year. The primary intended use of this dataset is to monitor the structural stability of the brain of participants for the duration of the study. Many quantitative measures of brain structure can also be derived and included in analyses, such as gray matter morphometry, tractography or measures of myelination. Cortical flat maps cut with TkSurfer 6.0.0 are provided with the freesurfer derivatives for visualization.

The MRI sequences are described in more detailed in [](Brain_anatomical_sequences) and [](Spinal_cord_anatomical_sequences), including pdfs of the Siemens exam cards.

Brain T1w, T2w and DWI were copied from the HCP aging and development protocol for Prisma MRI scanner.
Other sequences were selected and optimized by the Courtois NeuroMod team.

All images covering the face were anonymized by zeroing the data in the face, teeth and ears regions with a custom mask warped from the MNI space based on a linear registration of the T1w brain MRI series. This defacing script is available [here](https://github.com/courtois-neuromod/ds_prep/blob/main/mri/prepare/deface_anat.py)

## hcptrt

This `cneuromod` dataset is called HCP test-retest (`hcptrt`), because participants repeated 15 times the functional localizers developed by the Human Connectome Project, for a total of approximately 10 hours of functional data per subject. The protocol consisted of seven tasks, described below (text adapted from the [HCP protocol](http://protocols.humanconnectome.org/HCP/3T/task-fMRI-protocol-details.html)). Before each task, participants were given detailed instructions and examples, as well as a practice run. A session was typically composed either of two repetitions of the HCP localizers, or one resting-state run and one HCP localizer. The e-prime scripts for preparation and presentation of the stimuli can be found in the [HCP database](https://db.humanconnectome.org/app/action/ChooseDownloadResources?project=HCP_Resources&resource=Scripts&filePath=HCP_TFMRI_scripts.zip). Stimuli and e-prime scripts were provided by the Human Connectome Project, U-Minn Consortium (Principal Investigators: David Van Essen and Kamil Ugurbil; 1U54MH091657) funded by the 16 NIH Institutes and Centers that support the NIH Blueprint for Neuroscience Research, and by the McDonnell Center for Systems Neuroscience at Washington University. Note that in the `cneuromod` DataLad, functional runs are named `func_sub-<participant>_ses-<sess>_task-<task>_run-<run>`, where the `<participant>` tag includes `sub-01` to `sub-06`. For each functional run, a companion file `_events.tsv` contains the timing and type of events presented to the subject. Session tags `<sess>` are `001`, `002` etc, and the number and composition of sessions vary from subject to subject. The `<task>` tags are `restingstate`, `gambling`, `motor`, `social`, `wm`, `emotion`, `language` and `relational`, as described below. Tasks that were repeated twice have separate `<run>` tags (`01`, `02`).

:::{important}
The duration of BOLD series are slightly varying across participants and repetitions. If consistent length is required by analysis, series can be trimmed at the end to match duration, task being aligned to the first TR.
:::

### [Gambling](http://www.cognitiveatlas.org/task/id/trm_550b5c1a7f4db/)
`gambling` duration: approximately 3 minutes. Participants were asked to guess whether a hidden number (represented by a “?” during 1500ms) was above or below 5 [(Delgado et al. 2000)](https://doi.org/10.1016/j.neuroimage.2004.10.002). They indicated their choice using a button press, and were then shown the actual number. If they guessed correctly they were told they won money (+$1.00, `win` trial), if they guessed incorrectly they were told they lost money (-$0.50, `loss` trial), and if the number was exactly 5 they were told that they neither won or lost money ($0, `neutral` trial). Note that no money was actually given to the participants and, as such, this task may not be an accurate reproduction of the HCP protocol. The conditions were presented in blocks of 8 trials of type `reward` (6 `win` trials pseudo randomly interleaved with either 1 `neutral` and 1 `loss` trial, 2 `neutral` trials, or 2 `loss` trials) or of type `punishment` (6 `loss` trials pseudo-randomly interleaved with either 1 `neutral` and 1 `win` trial, 2 `neutral` trials, or 2 `win` trials). There were four blocks per run (2 `reward` and 2 `punishment`), and two runs in total.

### [Motor](http://www.cognitiveatlas.org/task/id/trm_550b53d7dd674/)
`motor` duration: approximately 3 minutes. This task was adapted from (Buckner et al. 2011; Yeo et al. 2011). Participants were presented a visual cue, and were asked to either tap their left or right fingers (event types `left_hand` and `right_hand`, resp.), squeeze their left or right toes (event types `left_foot` and `right_foot`, resp.), or move their tongue to map motor area (event type `tongue`). Each movement lasted 12 seconds, and in total there were 13 blocks, with 2 of `tongue` movements, 4 of hand movements (2 `right_hand` and 2 `left_hand`), and 4 of foot movements (2 `right_foot` and 2 `left_foot`), and three 15 second fixation blocks where participants were instructed not to move anything. There were two runs in total, and 13 blocks per run.

### [Language processing](http://www.cognitiveatlas.org/task/id/trm_550b54a8b30f4/)
`language` duration: approximately 4 minutes. Participants were presented with two types of events. During `story` events, participants listened to an auditory story (5-9 sentences, about 20 seconds), followed by a two-alternative forced-choice question. During `math` events, they listened to a math problem (addition and subtraction only, varies in length), and were instructed to push a button to select the first or the second answer as being correct. The task was adaptive so that for every correct answer the level of difficulty increased. The math task was designed this way to maintain the same level of difficulty between participants. There were 2 runs, each with 4 `story` and 4 `math` blocks, interleaved.

### [Social cognition](http://www.cognitiveatlas.org/task/id/trm_550b557e5f90e/)
`social` duration: approximately 3 minutes. Participants were presented with short video clips (20 seconds) of objects (squares, circles, triangles) that either interacted in some way (event type `mental`), or moved randomly on the screen (event type `random`) ([Castelli et al. 2000](https://doi.org/10.1006/nimg.2000.0612); [Wheatley et al. 2007](https://doi.org/10.1111/j.1467-9280.2007.01923.x)). Following each clip, participants were asked to judge whether the objects had a “Mental interaction” (an interaction that appeared as if the shapes were taking into account each other’s feelings and thoughts), whether the were “Not Sure”, or if there was “No interaction”. Button presses were used to record their responses. In each of the two runs, participants viewed 5 `mental` videos and 5 `random` videos, and had 5 fixation blocks of 15 seconds each.

### [Relational processing](http://www.cognitiveatlas.org/task/id/trm_550b5a47aa23e/)
`relational` duration: approximately 3 minutes. Participants were shown 6 different shapes filled with 1 of 6 different textures (Smith et al. 2007). There were two conditions: relations processing (event type `relational`), and control matching condition (event type `control`). In the `relational` events, 2 pairs of objects were presented on the screen, with one pair at the top of the screen, and the other pair at the bottom. Participants were instructed to decide what dimension differed in the top pair (shape or texture), and then decide if the bottom pair differed, or not, on the same dimension (i.e. if the top pair differed in shape, did the bottom pair also differ in shape). Their answers were recorded by one of two button presses: “a” differ on same dimension; “b” don't differ on same dimension. In the `control` events, participants were shown two objects at the top of the screen, and one object at the bottom of the screen, with a word in the middle of the screen (either “shape” or “texture”).They were told to decide whether the bottom object matched either of the top two objects on that dimension (i.e., if the word is “shape”, did the bottom object have the same shape as either of the top two objects). Participants responded “yes” or “no” using the button box. For the `relational` condition, the stimuli were presented for 3500 ms, with a 500 ms ITI, and there were four trials per block. In the `control`condition, stimuli were presented for 2800 ms, with a 400 ms ITI, and there were 5 trials per block. In total there were two runs, each with three `relational` blocks, three `control` blocks and three 16-second fixation blocks.

### [Emotion processing](http://www.cognitiveatlas.org/task/id/trm_550b5b066d37b/)  
`emotion` duration: approximately 2 minutes. Participants were shown triads of faces (event type `face`) or shapes (event type `shape`), and were asked to decide which of the shapes at the bottom of the screen matches the target face/ shape at the top of the screen (adapted from Smith et al. 2007). Faces had either an angry or fearful expression. Faces, and shapes were presented in three blocks of 6 trials (3 `face` and 3 `shape`), with each trial lasting 2 seconds, followed by a 1 second inter-stimulus interval. Each block was preceded by a 3000 ms task cue (“shape” or “face”), so that each block was 21 seconds long, including the cue. In total there were two runs, three `face` blocks and three `shape` blocks, with 8 seconds of fixation at the end of each run.

### [Working memory](http://www.cognitiveatlas.org/task/id/trm_550b50095d4a3/)  
`wm` duration: approximately 5 minutes. There were two subtasks: a category specific representation, and a working memory task. Participants were presented with blocks of either places, tools, faces, and body parts. Within each run, all 4 types of stimuli were presented in block, with each block being labelled as a 2-back task (participants needed to indicate if they saw the same image two images back), or a version of a 0-back task (participants were shown a target at the start of the trial and they needed to indicate if the image that they were seeing matched the target). There were thus 8 different event types `<stim>_<back>`, where `<stim>` was one of `place`, `tools`, `face` or `body`, and `<back>` was one of `0back` or `2back`. Each image was presented for 2 seconds, followed by a 500 ms ITI. Stimuli were presented for 2 seconds, followed by a 500 ms inter-task interval. Each of the 2 runs included 8 event types with 10 trials per type, as well as 4 fixations blocks (15 secs).

### [Resting state](http://www.cognitiveatlas.org/task/id/trm_4c8a834779883/)
`restingstate` duration: 15 minutes. In every other session, one resting-state fMRI run was acquired, giving 5 runs per participant. Participants were asked to have their eye open, be looking at fixation cross in the middle of the screen and be instructed to not fall asleep. A total of five resting-state fMRI runs were acquired per subject.

## movie10

This dataset includes about 10 hours of functional data for all 6 participants. The python & psychopy scripts for preparation and presentation of the clips can be found in `src/tasks/video.py` of the following github [repository](https://github.com/courtois-neuromod/task_stimuli).
Session tags `<sess>` were `001`, `002` etc, and the number and composition of sessions varied from subject to subject. The `<task>` tags used in DataLad corresponded to each movie (`bourne`, `wolf`, `life`, `figures`) and a numerical index of the segments shown as each movie was cut into roughly ten minutes segments presented in separate run. Exact cutting points were manually selected to not interrupt the narrative flow. Fade out to a black screen was added at the end of each clip, and with a few seconds overlap between the end of a clip and the beginning of the next clip. The movie segments can be found under `movie10/stimuli/<movie>/<movie>_seg<seg>.mkv`, and the functional runs are named `func_sub-<participant>_ses-<sess>_task-<movie><seg>`, where the `<participant>` tag ranges from `sub-01` to `sub-06`. A companion file `_events.tsv` contains the timing and type of conditions presented to the subject.

The participants watched the following movies ([cogatlas](https://www.cognitiveatlas.org/id/trm_4c898da401420/)):
 * `<task>` name `bourne`: [The Bourne supremacy](https://en.wikipedia.org/wiki/The_Bourne_Supremacy_%28film%29). Duration ~100 minutes.
 * `<task>` name `wolf`: [The wolf of wall street](https://en.wikipedia.org/wiki/The_Wolf_of_Wall_Street_%282013_film%29). Duration ~170 minutes.
 * `<task>` name `figures`: [Hidden figures](https://en.wikipedia.org/wiki/Hidden_Figures). Duration ~120 minutes. This movie was presented twice, for a total duration of ~240 minutes.
 * `<task>` name `life`: [Life](https://en.wikipedia.org/wiki/Life_(British_TV_series)) Disc one of four: "Challenges of life, reptiles and amphibian mammals". DVD set was narrated by David Attenborough. Duration, and lasted ~50 minutes. This movie was presented twice, for a total duration of ~100 minutes.

It should be noted that although three of the participants are not native anglophones, all participants watched the movies in English. The three native francophone participants are fluent in English and report regularly watching movies in English.



:::{important}
The duration of BOLD series are slightly varying across participants and repetitions. If consistent length is required for analysis, series can be trimmed at the end to match duration, movie segments being aligned to the first TR.
:::


:::{important}
There are instances of re-scanned segments (due to scan QC fail), these re-scans will be in separate sessions. These should be handled or excluded in analysis requiring continuity of the presentation of the story.
:::

## Friends

This dataset contains functional data acquired while showing participants episodes of the Friends TV show in English. It includes seasons 1-6 for all subjects, except `sub-04` who only completed seasons 1-4 (and a few segments of season 5). Each episode is cut in two segments (a/b) to allow more flexible scanning and give participants opportunities for breaks. There is a small overlap between the segments to allow participants to catch up with the storyline. The task BIDS entity identifies the season, episode and segments (a/b) as such `task-s<eason>e<pisode>[ab]`.

:::{important}
A mistake happened when the pilot episode (`s01e01`) was accidentally skipped at the beginning of the first season. It was shown to participants after they had watched episodes `s01e02` to `s01e06`, causing a slight disruption in the storyline. In the latest release, files have been renamed to match the episodes' intended order (rather than the order in which they were administered) and to be consistent with external data such as annotation corpora.
:::


## harrypotter

This dataset contains a single session per participant (N=5) when they read chapter 9 from chapter 9 of Harry Potter and the Sorcerer’s Stone. The text was presented word by word, at a 2Hz pace (each word presented for .5s). This chapter was split over 7 runs of approximate equal length. The stimuli used in this dataset are taken from the experiment reported by [Wehbe et al. (2014)](https://www.biorxiv.org/content/10.1101/2020.09.28.316935v4.full.pdf#cite.wehbe2014) for which a separate fMRI dataset (N=9) has been collected and shared.

## gamepad

This dataset was acquired as a validation study of the CNeuroMod videogame controller. The CNeuromod videogame controller is an open source, custom-built, fiber-optic, MRI compatible video game controller, designed by our team engineer, Mr. André Cyr, and described in [Harel et al. (2023)](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0290158). For a detailed description of the controller, including building instructions visit this [site](https://controller-doc.readthedocs.io/en/latest/). The gamepad dataset contains both fMRI and behavioural data acquired on 4 participants (`sub-01`, `sub-02`, `sub-03` and `sub-06`) during a simple cued-response task in which the participants were instructed to press the various controller buttons for short and long durations (5 blocs of 10 trials per condition).

For each subject we acquired 8 sessions, of two runs each. Four of the sessions were acquired in the MRI scanner using our typical setup (i.e 64-channel head coil) along with the MRI-compatible videogame controller, during which we acquired BOLD recordings. The four remaining sessions were acquired in our MRI [simulator](https://pstnet.com/products/mri-simulator/), with a mock 64-channel head coil, and using a [commercially available SNES-like controller](https://lyonsden.net/innext-usb-game-controller-review/). The latter served as a reference for our validation study. Mock and MRI sessions were alternated, and the starting order (mock or MRI first) was counterbalanced across subjects. For the MRI sessions, the behavioural data can be found in the `*_events.tsv` files stored in the `func` folder. For the mock sessions, behavioural data can be found in the `beh` folder.

## shinobi_training

This is a pure behavioral dataset collected while participants trained at home on the videogame Shinobi III The Return of the Ninja Master.
A subset of 3 levels of the game was selected for their similarity in terms of core gameplay although some mechanics were specific to each level. These levels were the same than those used in the [`shinobi`](https://docs.cneuromod.ca/en/latest/DATASETS.html#shinobi) dataset.

The participants were first introduced to the game by playing the Level-1 at least once. This level introduces the basic game mechanics (moving from left to right, avoid or kill enemies) at an abordable difficulty level for most players. Then, the participants were able to freely choose the level on which they played as well as the training sessions frequency. No training regimen was imposed to the participants making that dataset highly heterogeneous. The dataset consists of sessions of gameplay as collections of `.bk2` files recorded by the [gym-retro](https://github.com/openai/retro) API.

This dataset can be used to analyze learning or individual game-play styles, and can be investigated in conjunction with the fMRI dataset.

The following table summarizes the volume of data acquired per subject and per level, including the total number of repetitions for each level, the number of cleared repetitions, and the corresponding play time.
|         | Level 1      |            |              | Level 4      |            |              | Level 5      |            |              | Total       |            |              |
|---------|--------------|------------|--------------|--------------|------------|--------------|--------------|------------|--------------|-------------|------------|--------------|
| Subject | N            | Cleared    | Duration (h:m:s) | N            | Cleared    | Duration (h:m:s) | N            | Cleared    | Duration (h:m:s) | N           | Cleared    | Duration (h:m:s) |
| sub-01  | 187          | 116        | 07:34:10     | 110          | 24         | 03:02:11     | 116          | 43         | 05:00:30     | 413         | 183        | 15:36:53     |
| sub-02  | 263          | 52         | 12:56:22     | 290          | 75         | 10:40:20     | 51           | 17         | 02:58:26     | 604         | 144        | 26:35:09     |
| sub-04  | 57           | 2          | 03:56:12     | 98           | 14         | 05:32:58     | 57           | 13         | 03:13:22     | 212         | 29         | 12:42:33     |
| sub-06  | 9            | 3          | 00:42:43     | 36           | 7          | 01:48:47     | 32           | 8          | 01:44:54     | 77          | 18         | 04:16:25     |
| Total   | 516          | 173        | 25:09:28     | 534          | 120        | 21:04:18     | 256          | 81         | 12:57:14     | 1306        | 374        | 59:11:01     |


## shinobi

This dataset contains about 8h of gameplay on the videogame Shinobi III The Return of the Ninja Master for N=4 participants (`sub-01`, `sub-02`, `sub-04` and `sub-06`). To limit the impact of learning on the `shinobi` dataset, fMRI data were acquired after an initial training phase (constituting the [`shinobi_training`](https://docs.cneuromod.ca/en/latest/DATASETS.html#shinobi-training) dataset) where the subjects were introduced to the game content outside the MRI scanner. Thus, the `shinobi` dataset contains fMRI and behavioral gameplay data during a phase of relatively stable performance, providing a rich and naturalistic dataset suitable for cognitive neuroscience and imitation learning research.

Participants used the CNeuromod videogame controller described in [Harel et al. (2023)](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0290158). In each run, participants played 3 levels in cycles and always in the same order. These levels were selected in the game to have fairly homogeneous core game mechanics (see the [Sega documentation](https://sega.fandom.com/wiki/Shinobi_III:_Return_of_the_Ninja_Master) for more details on game structure):
 * `Level-1` corresponded to round 1 of the original game, "Zeed's Resurrection". It included one mini-boss and one boss fight.
 * `Level-4` corresponded to the beginning of round 4 of the original game, "Destruction". It included no mini-boss or boss fight.
 * `Level-5` corresponded to the beginning of round 5 of the original game, "Electric demon". It included one mini-boss fight and no boss fight.

Participants moved to the next level if they successfully completed a level, or lost three lives. A new level was then initiated unless 10 minutes had elapsed from the start of the run, at which point the run ended. The duration of each run is thus variable to a degree, with a minimum of ten minutes. Due to the fixed order in the cycle, `Level-1` was repeated more often than `Level-4` and `Level-5`.

In this dataset and the related documentation, we use the term `run` to designate a single functional sequence acquisition (per the usual in neuroimaging). The term `repetition` is used to designate the play of a single level (from start to either completion or the loss of three lives). As such, each run contains around 3 to 5 repetitions.

For each functional run, a companion file `_events.tsv` contains the timing and duration of each repetition played, as well as a `_annotated_events.tsv` file that additionally contains richer annotations, including button presses, handcrafted annotations (Kills, Health losses), and frame-wise RAM values. Additional documentation on the available annotations can be [found here](https://github.com/courtois-neuromod/shinobi/blob/annotations/code/annotations/ANNOTATIONS.md).

The companion `.bk2` files can be found in the `<participant>/<sess>/gamelogs` folder.

The following table summarizes the volume of data acquired per subject and per level, including the total number of repetitions for each level, the number of cleared repetitions, and the corresponding play time.
|         | Level 1      |            |              | Level 4      |            |              | Level 5      |            |              | Total       |            |              |
|---------|--------------|------------|--------------|--------------|------------|--------------|--------------|------------|--------------|-------------|------------|--------------|
| Subject | N            | Cleared    | Duration (h:m:s) | N            | Cleared    | Duration (h:m:s) | N            | Cleared    | Duration (h:m:s) | N           | Cleared    | Duration (h:m:s) |
| sub-01  | 89           | 84         | 03:57:26     | 64           | 44         | 01:59:50     | 53           | 53         | 02:05:44     | 206         | 181        | 08:03:01     |
| sub-02  | 81           | 76         | 03:41:53     | 58           | 30         | 02:11:49     | 55           | 47         | 02:37:34     | 194         | 153        | 08:31:16     |
| sub-04  | 70           | 67         | 03:26:50     | 56           | 29         | 02:06:00     | 53           | 47         | 02:39:47     | 179         | 143        | 08:12:39     |
| sub-06  | 46           | 45         | 03:29:24     | 42           | 23         | 02:44:22     | 13           | 12         | 00:48:59     | 101         | 80         | 07:02:45     |
| Total   | 286          | 272        | 14:35:34     | 220          | 126        | 09:02:02     | 174          | 159        | 08:12:06     | 680         | 557        | 31:49:43     |


:::{important}
Due to a programming error a certain number of game recording files were lost during acquisition, these repetitions are still listed in the events file but their `stim_file` field is left blank. Choice is left to the user whether to exclude the corresponding fMRI volumes or not for their analysis.
:::

## things

N=4 participants completed between 33 (`sub-06`) and 36 (`sub-01`, `sub-02`, `sub-03`) fMRI sessions of a continuous recognition task with images from the [THINGS dataset](https://things-initiative.org/). The first session included 3 runs, and all subsequent sessions included 6 runs. Each 4.7 minutes run included 60 trials. For each trial, an image was shown in the center of the screen for 2.98s, followed by a 1.49s ISI. Subjects maintained fixation on a black fixation marker overlaid onto the image center and visible at all times throughout a run. Images were sampled from 720 THINGS categories. `sub-01`, `sub-02`, `sub-03` were shown 6 images per category (4320 unique stimuli), and `sub-06` was shown 5 images for 480 categories and 6 images for the remaining 240 (3840 unique stimuli).  

Each image was shown three times throughout the duration of the experiment (it was repeated once within and once across weekly sessions). For each trial, participants reported whether the image was shown for the first time (“unseen”) or whether it had been shown previously (“seen”), either during the current or a previous session or both. Participants also reported whether or not they felt confident in their answer. Responses (seen/unseen ✕ low/high confidence) were made with the right thumb by pressing one of four buttons (top, bottom, left, right) on a video game controller designed by the team and described in [Harel et al. (2022)](https://psyarxiv.com/m2x6y/). No feedback was given to participants throughout the entire duration of the experiment.

For each functional run, a companion file `_events.tsv` contains the timing and duration of each trial, the identity of the image shown, the condition (seen/unseen), whether the image was repeated between and/or within session, the subject's response and whether it was correct, the delay and number of trials since the last presentation (for repeating items), and metrics of fixation compliance derived from eye-tracking data. Available trial annotations are described [here](https://github.com/courtois-neuromod/things_memory_results/blob/marie_dev/src/behav_data/events_descriptors_wEyetrack.json)

:::{important}
A few sessions were accidentally administered out of the planned order, introducing atypical patterns of repetition for images shown during/after those sessions. Users may want to exclude these sessions from analyses that depend on repetition patterns or memory performance. These include `ses-024`, `ses-025` and `ses-026` for `sub-03`, and `ses-019` to `ses-026` (inclusively) for `sub-06`. fMRI data from `run 6` of `sub-06`'s `ses-008` are excluded from the dataset due to mistakenly positionned MRI field-of-view.
:::

## retinotopy

Three participants (`sub-01`, `sub-02`, `sub-03`) completed multiple sessions (6 for `sub-01` and `sub-02`, 5 for `sub-03`) of a retinotopy task adapted from [Kay et al. (2013)](https://doi.org/10.1152/jn.00105.2013) and implemented in Psychopy. This task was designed to derive population receptive field (pFR) properties at the voxel level and to delineate ROIs from the early visual cortex.

Each session included three 5-minutes functional runs, each of which used a different aperture shape : `ring`, `bar` or `wedge`. A run included eight cycles during which an aperture moved slowly across the stimulated visual field to reveal a portion of visual pattern designed to drive both low-level and high-level visual areas. Patterns were drawn randomly at a rate of 15 fps from the [Human Connectome Project retinotopy stimuli](https://doi.org/10.1167/18.13.23) (downloaded [here](http://kendrickkay.net/analyzePRF)).

The stimulated visual field was a circular area with a diameter corresponding to 10 degrees of visual angle. `ring` runs featured a thick circle aperture that expanded from and contracted toward the screen center. `wedge` runs featured a wedge aperture rotating clockwise and counter-clockwise. `bar` runs featured a wide bar aperture sweeping across the screen in 8 different directions. Participants fixated their gaze on a central dot and pressed a button whenever the dot changed color (alternating between blue and orange).

## floc

Three participants (`sub-01`, `sub-02`, `sub-03`) completed six sessions of a functional localizer task designed to identify brain regions responding preferentially to specific stimulus categories. The task was based on a [Psychopy implementation](https://github.com/NBCLab/pyfLoc) of the [Stanford VPN lab's fLoc task](https://doi.org/10.1523/JNEUROSCI.4822-14.2015) using stimuli from the fLoc functional localizer package (downloaded [here](https://github.com/VPNL/fLoc)).

Each session included two functional runs of 3.85 minutes with randomly ordered ~6s blocks of rapidly presented images from one of five categories : `faces`, `places`, `bodies`, `objects` and `characters`. Each block included 12 trials for which an image from the block’s category was displayed centrally for 0.4s, followed by a 0.095-0.1s ISI. Subjects were instructed to fixate on a red dot in the middle of the screen and to press a button whenever the same image appeared twice in a row (the “one-back” task variation). Blocks of baseline condition during which the red fixation dot appeared on a grey background for 5.96s were also intermixed in the block sequence. Each run included 6 blocks from each of the five categories and 6 blocks of baseline. For each session, the first run included images from the house (`places`), body (`body parts`), word (`characters`), adult (`faces`) and car (`objects`) fLoc package sub-categories. The second run included images from the corridor (`places`), limb (`body parts`), word (`characters`), adult (`faces`) and instrument (`objects`) sub-categories.
