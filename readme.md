## Wainwright Panel
Panel dependency

## Speech Perception Task
=======================
**Last updated in PsychoPy version 2021.2.3**

*To Do:*

- think of new joke and make images for breaks for session 2
- make an instructions video for the threshold part of the task
- pilot task for task durations and data output
- measure volume of babble and movie with a decibel meter to get an approximate idea of what volumes correspond to in dB

Run link: https://run.pavlovia.org/lpxrh6/code_crackers/

Adapted runLink with query strings:
- Run link session 1: https://run.pavlovia.org/lpxrh6/code_crackers/?session=1
- Run link session 2: https://run.pavlovia.org/lpxrh6/code_crackers/?session=2&baseline_corr=2 (baseline_corr should correspond to the average accuracy in session 1 expressed as a rounded integer between 1 and 4)

If using this task please cite: Turoman, N., Hirst, R.J, & Stacey, J. E. (2021, October 10). Do Masks Effect The Perception of Speech In Noise? Retrieved from osf.io/56x9r

Task Description
-----------------
This is an assessment of speech perception. The task is divided into two parts, baseline assessment and threshold assessment.

*Baseline assessment* 
----------------------
Sentences are presented in the absence of any noise. The purpose of this task is to obtain average accuracy for the participant so that this is then used as the cut-off for accuracy in the speech-in-noise task. For example, if a participant scored an average of 2 out of 4 words correct at baseline, they would need to obtain a score of 2 or higher on each trial in the threshold task for that to be classes as "correct".

On each trial participants are presented with a varied ITI in which a fixation is presented. In this time, the movie is loaded, the duration of the ITI will vary depending on loading time, but is saved to file (exact range will be reported on write-up). Following this, the participant is presented with a movie of a speaker reading one of 30 keyword sentences, each sentence lasts around 4 seconds and contains 4 keywords. The speaker will be presented in one of 2 conditions, wearing a surgical mask or not wearing a mask, thus, there are 60 sentences in total. Stimuli are presented in a pseudo-random order in which half of the sentences are presented first for the masked condition and half for the no mask condition - eliminating an influence of prior exposure on either condition. Following sentence presentation the participant is presented with an array of 8 images, 4 keyword images and 4 flanker images. The 4 flanking images for each trial were first randomly selected and then screened by the author to eliminate any instances where a flanking image held close similarity to a keyword image. 

*Threshold assessment* 
------------------------
An interleaved staircase procedure in which sentences are presented in multi-talker babble. On each trial the volume of the sentence (the signal) will decrease or increase in a one-up-one-down procedure; following correct or incorrect responses respectively. Each staircase will end either when the maximum number of trials has been reached (30 per sentence)  or `maxReversals` has been reached (currently `maxReversals = 7`). On each trail a correct/incorrect response is classified as scoring equal or greater than baseline performance.

To control parameters of the staircase use `update_stair` routine `stairUpdate` component:
```
	startVol = 0.2 # starting volume of the signal
	stepSize = 0.05 # stepsize of the signal
	# How many reversals until we consider a staircase complete
	maxReversals = 7
```
Data output 
------------------------

Relevant to both tasks:
- `sentence`: the sentence presented
- `mask`: video with mask or no mask
- `keyword_0` - `keyword_3`: the keywords in the sentence
- `flankword_0` - `flankword_3`: the flanking images presented with that sentence image set
- `clicked_images`: name of the images selected.
- `corrCount`: how many images selected were correct.
- `incorrCount`: how many images selected were incorrect.
- `fixation_time`: how long the fixation was presented for (how long it took the movie to load)
- `mouse.time`: the time of each mouse click relative to the routine start time.
- `mouse.clicked_name`: the name of the components clicked (corresponding to mouse times in `mouse.time`)

Relevant to baseline task:
- `running_average`: the running average of nCorrect. 
- `baseline_corr`: `running_average` but as an integer value rounded to 0 decimal places  **
- `custom_url`: The url for session 2 to use for this participant 
Note: the final value should be used in the "baseline_corr" parameter when running the second session**

Specific to thresholding task:
- `staircase1_threshold`: the threshold obtained for this staircase either by averaging the last 7 reversals or averaging the reversals that did occur.
- `staircase1_finalReversals`: the number of reversals that occurred in this stair (how many were used to create the threshold)
-`staircase1_name` - name of current staircase (mask or no mask)
- `staircase1_volume` - volume of the signal on the current trial (arbitrary PsychoPy unit 0 - 1)
- `staircase1_SNR` - volume of signal / volume of noise both values in PsychoPy units 0 - 1
- `staircase1_reversals` - number of reversals so far in this staircase
- `staircase1_direction` - direction of current vol (increasing - up or decreasing - down)
- `staircase1_complete` - if the current staircase is complete

Stimuli
------------------------

- **Sentence stimuli:** All sentences were sampled from Brown et al. (2021). Videos were recorded with a Huawai P30lite camera phone and audio recorded with a Blue Yeti mic. Audio file amplitudes were normalized using Praat version 6.1.50 (Boersma, Paul and Weekink (2021) (using Katherine Crosswhite's stimulus intensity script - see resources). Audio and video streams were synced using Praat to detect an auditory event in both recordings (a clap occurring ~1 second prior to voice onset) then video audio was replaced with higher quality mic audio using ffmpeg (Tomar, 2006). All scripts used to process auditory and video stimuli can be found here https://github.com/RebeccaHirst/AVsync. Because the current study implemented picture matching response rather than vocal responses at used by Brown et al. (2021), a subset of sentences were chosen for which keyword images were created, where the keywords were commonly used in English rather than American English (e.g. sentence using the word “garbage” was excluded) and for which the keywords were considered non-ambiguous enough for children.
- **Babble stimuli** Five samples of two-speaker babble were created. Babble speakers were two female speakers (selected to closely match the primary speaker). The babble sentences did not contain any of the keywords. (babble script in subfolder Stimuli/babble/babble_script.doc). On each trial, the babble sample was pseaudorandomly selected, the babble paired with each stimulus was the same for all participants and each babble sample was selected to occur the same number of times within the mask and no mask conditions (see "babble" column in "threshold_conditions.csv")
- **Keyword image stimuli** Images were custom drawn for each keyword by the author, Nora Turoman. Following each trial 8 images were presented, 4 images corresponding to the 4 keywords in the sentence and 4 “flanker” images. Flanker images were selected and reviewed by the authors on the basis of resemblance to keywords (i.e.  if the sentence contained the word “cheap” it was ensured a picture for the keyword “money” was not presented, since these are closely related). The same image sets were used across mask conditions and across participants.

References and Resources
-----------

Brown, V. A., Van Engen, K. J., & Peelle, J. E. (2021, March 12). Face mask type affects audiovisual speech intelligibility and subjective listening effort in young and older adults. https://doi.org/10.31234/osf.io/7waj3

Crosswhite, K. (2009) Adjust-Intensity. Computer Program. *Retrieved from: Praat Script Resources* http://phonetics.linguistics.ucla.edu/facilities/acoustic/praat.html  

Hirst, R.J. (2021) Audio-Visual Sync. Computer Program. *Retrieved from:* https://github.com/RebeccaHirst/AVsync

Tomar, S. (2006). Converting video formats with FFmpeg. Linux Journal, 2006(146), 10.