---
layout: post
title: Clinical Documentation - 2020
categories: [Clinical Documentation]
tags: featured

---

#### Sections in this article
{:.no_toc}
* TOC
{:toc}

# Set up & procedures
This section contains information on set up for specific equipment that may have been learned by clinical team through experiments. This does not contain very general information for such equipment that can be contained in a manual.

## Wearable Sensing VR300
Refer to manual for general set up

### Signal quality issues with cap
* The VR300 is a sparse-array dry-electrode one-size-fits-all cap with linked-ear reference/ground (clips). The primary difficulty observed by the clinical team with application of the VR300 has been difficulty fitting the cap on persons with particularly small/large or oblong-shaped heads. F7 and Fz electrodes are relatively free-floating, but the Pz/P4/PO7/PO8/Oz complex is rigidly fixed to a single plastic lattice at the back of the unit. If any of these electrodes are "floating", then they will be more susceptible to ambient electrical noise, EMG, etc. Posterior electrodes in particular will record neck EMG if a participant is sitting in a strained position and electrode contact(s) is/are bad.
* Because the shape/fit of the cap is static and does not always work well for certain head shapes, pressure differences cause a plethora of issues. Cardioballistic artifact (CBA; visible heart beat) will appear if an electrode is pressed too tightly against a blood vessel.

### Troubleshooting signal quality issues
* Make sure ear clips are properly attached to earlobes. The more surface area each clip touches, the better the signal. Clean earlobes with alcohol or water and let dry, if needed.
* Fitting is a primary concern for this unit. Set the cap as far forward as you can when fitting (front strap edge should sit 1-2 cm above eyebrow ridge), but make sure you can observe contact with Pz and the scalp. If Pz is "floating" above the hair/skin, push the cap down and slide back only as much as necessary to get good contact with Pz.
* When first placing cap, electrodes will be "turned" to shift hair and establish skin contact. After an initial 1-2 passes of turning electrodes, focus instead on applying pressure to electrodes. Holding pressure for as long as 1 minute is sometimes necessary. Only turn electrodes as necessary (i.e., pressure is still not helping the signal).

### Special considerations for cap
* The shape of the unit sometimes applies too little pressure to the posterior sites, but also sometimes applies too much pressure to Fz/F7, causing discomfort. Make sure to monitor these sites as such and also brush hair away from the forehead under F7, as needed.
* The bulky shell of the VR300 makes alignment difficult. When fitting the cap, do your best to put the unit on straight, then stand ~5-6 feet in front of the participant and ask them to look straight ahead and lower their chin to their chest (if able). Visually confirm alignment of the midline electrodes (i.e., Fz and Pz).
* Our version of the cap utilizes a modified montage in the DSI Streamer software (where we check signal quality before initiating BciPy testing; a montage is just a list of electrodes w/ placement info). Sometimes you might notice a difference in how the signal looks via the DSI streamer when compared to the BciPy EEG viewer. This variance is possibly related to the referencing mechanisms involved in either display. The DSI streamer montage from Wearable currently designates P4 as the common reference for all scalp electrodes. Our BciPy system uses the linked-ear clips as a reference instead. As such, make sure in particular that the signals look good for A1/2 and P4 in the Wearable DSI streamer before moving to BciPy (ideally everything will look good in both, but this item is particularly important).

## Wearable Sensing DSI-24
Refer to manual for general set up

### Signal quality issues with cap
The DSI24 is a dry-electrode one-size-fits-all cap with linked-ear reference/ground (clips). Signal quality issues have been observed with several users, though these have typically been resolvable by adjusting the cap (e.g. tightening the click wheel) or electrodes. Cardioballistic artifact (CBA; visible heart beat) will appear if an electrode is pressed too tightly against a blood vessel.

### Troubleshooting signal quality issues
* Make sure ear clips are properly attached to earlobes. The more surface area each clip touches, the better the signal. Clean earlobes with alcohol or water and let dry, if needed.
* When first placing cap, electrodes will be "turned" to shift hair and establish skin contact. After an initial 1-2 passes of turning electrodes, focus instead on applying pressure to electrodes. Holding pressure for as long as 1 minute is sometimes necessary. Only turn electrodes as necessary (i.e., pressure is still not helping the signal).
* Sweat may reduce signal quality. Use a fan or other means to cool down the person wearing the cap, if necessary.

### Special considerations for cap
* This cap may cause discomfort or pain for some users. This seems to happen more frequently for users with smaller heads. Sometimes the pain can be alleviated by loosening the click wheel on the band without reducing signal quality.
* As of March 2020, the DSI24 does not tighten evenly on the sides as you turn the click wheel. This can lead to either the frontal electrodes becoming off center or T3 and T4 not being symmetrically placed above the ears.

### Population-specific considerations
* Because the cap can cause discomfort or pain for some users, take care when using the cap with people with communication impairments who may not be able to easily alert you to their discomfort. Be sure to ask frequently (perhaps every 5 minutes or during every break during or between tasks) if they are experiencing pain or discomfort. If the discomfort cannot be alleviated by adjusting the cap, the session must be cut short.
* The cap has a bulky area at the back of the head which contains several electrodes. Pay close attention to changes in signal quality during head movements when the user is lying in bed or resting against a wheelchair headrest.

*This section was last updated by Deirdre McLaughlin, Betts Peters, and Dan Klee in April, 2020. This information will be updated at 3-4 month intervals*  

# Design and data summaries from recent experiments
This section contains data and information for formal and informal experiments conducted from 2018-2020.

## BCI R01 Alzheimer's Disease Supplement

### Technology

#### Hardware

VR300 cap by Wearable Sensing

>Notes:
* This cap was modified from standard design to remove electrode at P3 and change it to F7.
*Participants 1 & 2 utilized an unmodified (aside from F7) version of the VR300 unit. Antiquated design elements compared to current market version as of April, 2020. Tightening knob placed at top of spinal column, under Oz, and it tightened side straps. Built-in lock-and-key adjustment knobs. F7 electrode capsule oversized (same as P3 capsule), which caused pressure and discomfort
Participants 3-5 utilized a modified version of the VR300
Design updated to more closely resemble the current market version as of April 2020. Tightening knob moved to top of cap (~Cz location), and it now tightens front/center plastic wing (Fz). Side straps bolted in place
F7 capsule changed out for a smaller version to decrease pressure on forehead.

Laptop: ASUS Vivo-book
>* NAME: LAPTOP-92PLCQNR
* CPU: Intel i7-8565U @ 1.80 GHz 1.99 GHz
* RAM: 16.0 GB
* GPU: NVidia GEFORCE GTX

#### Operating System

Windows 10 Pro 64 Bit

#### Software

BCIPy RSVP 1.4.2
> Notes: Custom uncommitted modifications made in-line for power spectral density elements in feedback calibration, including additional notch filters for 60-Hz alias and harmonic artifact selectable character set that will include/exclude < and _ as desired for older participants Online computation of relative PSD in feedback calibration will utilize only the filtered spectrum in the denominator (e.g., 2-45 Hz or 7-20 Hz, in most cases), rather than a filtered version of the entire visible spectrum (e.g., 0-150 Hz after downsampling a VR300 recording by a factor of 2). Number of commits: 4. Unique commit identifiers: e9a37f8 (Aug - Sept, 2019)
68c00f8 (Sept - Nov. 2019)
c9f7a3f (Nov - Dec. 2019)
f2ff6d0 (Jan - Mar 2020)

#### Filters
Standard Calibration
* Bandpass 2-45 Hz
* Notch @ 60 Hz
* Order 2
* Down-sample rate of 2

Copy Phrase
* Bandpass 2-45 Hz
* Notch @ 60 Hz
* Order 2
* Downsample rate of 2

Feedback Calibration
* Bandpass 7-20 Hz
* Notch @ 60 Hz
* Order 8
* Downsample rate of 2
* Feedback lower bound: Depends (typically 8 Hz)
* Feedback upper bound: Depends (typically 10 Hz)

> Note: Standard calibration tasks won't query filters while in-task (the purpose of this module is to record responses, not process them). As such, best practice here is to leave filter settings the same as in copy-phrase, so you won't have modify them between calibration -> copy-phrase.

### Data Set

#### Design
single case research design (non-experimental)

#### Sample size
n = 5

#### Participant Diagnosis
People with mild probable Alzheimer's Disease pathology

>Notes: MoCA greater than/equal to 14; OR MMSE, language-related impairment by clinical judgment from SLP

#### Age range
~50-80 years old
> Notes: IRB clearance for up to 100 years old

#### Number of recordings
baseline recordings: 27 recordings (calibration, copy phrase tasks)

intervention recordings: 42 recordings (calibration with feedback, copy phrase tasks)

follow up visit recordings: 2 recordings (calibration with feedback, copy phrase tasks)

#### raw data file types
.csv, .txt, .log, .xlxs

#### data location
Z:\BCI-AD Supplement\Data 

> Note: Oken network drive - need permission to access data; mapped to R:\ on most Oken lab machines) 

#### potential considerations/limitations
* copy phrase was discontinued after two incorrect selections
feedback was delivered by electrode with best signal quality and visually identifiable posterior alpha (varied by participant; typically P4 or Pz)
* Feedback cutoffs were modified actively throughout intervention. Specifically, week 1 values were taken after aggregating all useable baseline data. Each subsequent week, cutoffs were updated to reflect data from the previous week of intervention (e.g., week 3 cutoffs are estimated from week 2 data).
* data collection was discontinued at end of baseline for 2 participants and treatment/intervention for 1 participant given COVID policies

## BCI R01 Drowsiness 2 experiments
More to come! documentation in progress (April, 2020)

## BCI R01 Shuffle Speller experiments
More to come! documentation in progress (April, 2020)

*This section was last updated by Deirdre McLaughlin, Betts Peters, and Dan Klee in April, 2020. This information will be updated at 3-4 month intervals*

# Clinical Testing Results of System Features
In this section, members of the clinical testing team will put recent data on tested features of the BCIpy system. These will be organized into major concern areas

## Timing of system
This relates to verifying multiple system components accurately align temporally when new hardware or software is introduced or new environmental conditions are present

### Timing verification testing for version 1.4.2

#### Project:
RSVP

#### Date:
9/11/2019

#### Person responsible for testing:
Dan Klee

#### Outcomes:
DK ran tests on all computers using diode (LSL) and log (TXT) info and compared that to output from analogous timing module recordings. Timing output will be reflective of the static offset, which we have assumed to hover around 100 ms (0.100 sec).

#### Important Details:
NA

#### Figures:
This needs to be updated when functionality confirmed on Git Hub. Dan included spreadsheet with documentation results

### Feature tested: streamer latency testing of version 1.3.9 

#### Project:
RSVP

#### Date:
2/28/2019

#### Person responsible for testing:
Dan Klee

#### Outcome:
There seemed to be a difference of ~0.5 sec between the offset estimated in the code and the offset measured by the photo diode at the start of each session, regardless of session type. I’m not sure why this is, but it’s curious that this difference shrunk to ~0.1 sec once the actual trials began. It’s encouraging too that this 100 ms difference was closer to the original python estimation, and that offsets appeared to be more or less stable across trials.
 
As for the viewer, things are also a bit unclear. In the normal calibration task there appeared to be an increase in latency approximately 700 ms. In the neurofeedback calibration this increase was much smaller (approximately 50 ms). These differences were similar, whether you measured offset via the code or with the diode.

#### Important Details:
NA
#### Figure(s):
N/A

### Feature tested: timing testing version 1. .

#### Project:
RSVP

#### Date:
4/12/2019

#### Person responsible for testing:
Dan Klee

#### Outcome:
I looked at a sample of stimuli from 10 sequences in each task to see if this 100ms remainder still seems reasonable. Due to conditional stimulation of the photo diode, I could only pick certain sequences, but I did try to pick sequences evenly from throughout the recordings. Averaging these 10 trials/task together, it seems like our static offset should be measured a bit below 100 ms.
If we’re using the lsl triggers for our analyses, I feel less worried about timing issues, although I would like to do a check with Matt’s viewer on the two CP recordings I have in order to make sure. The triggers.txt markers seem more variable, and there does appear to be a between-task difference if we look at the triggers.txt values, though not in the direction I personally anticipated (I would have thought the language model might have added to the latency…).
 
#### Important Details:
NA

#### Figure(s):
NA

## Feedback for calibration task  

### Feature tested: functionality testing for feedback calibration (v. 1.4.2)

#### Project:
RSVP
#### Date:
9/23/2019
#### Person responsible for testing:
Dan Klee

#### Outcome:
I ran a normal calibration session at a flash rate of 3 Hz (verified w/ Deirdre’s script) to double-check that my posterior alpha rhythm was still ~8 Hz, and that there was no overlap with the SSVEP or the supposed harmonic at 6 Hz. I completed a full feedback calibration with my personalized cutoffs. I made sure the directionality of the feedback was appropriate for alpha-based feedback, and I verified these settings periodically by closing my eyes during select sequences (every eyes-closed sequence resulted in level 1 “worst” feedback). Eyes-open/attentive trials seemed to result largely in level 4 and level 5 feedback, though I have not reviewed the log file yet. I was fairly sleepy, so I noticed a fair number of level 2 and level 3 feedback as well. To be clear, this was the “best” feedback session I have personally completed to date. That is, the feedback seemed to reflect my subjective impressions of my performance much more accurately than in past pilot sessions.
Feedback appears to be tied to Oz in BciPy. We would ideally have a way of picking the feedback electrode, just like in the psd_explore script. I have created a ticket in pivotal tracker. The –feedback_desc true/false argument in Tab’s updated bcipy_psd_explore.py script doesn’t do quite what we need it to do. We have a workaround for the time being, but I can talk with Tab about this point some more (I don’t think I communicated very well when we first discussed the matter).

#### Important Details:
NA
#### Figure(s):
N/A

*This section was last updated by Deirdre McLaughlin, Betts Peters, and Dan Klee in April, 2020. This information will be updated at 3-4 month intervals*