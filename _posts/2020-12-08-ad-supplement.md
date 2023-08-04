---
layout: post
title: Alzheimer's Disease Supplement
categories: [Clinical Documentation]
tags: Alzheimer's Disease, BCI, Brain-Computer Interface, VR300, Wearable Sensing, VR300, clinical, documentation, clinical documentation, clinical study, clinical research, research, study, trial, experiment, supplement
author: [Deirdre McLaughlin, Betts Peters, Dan Klee]

---

#### Sections
{:.no_toc}
* TOC
{:toc}

*This section was last updated by Deirdre McLaughlin, Betts Peters, and Dan Klee in April, 2020. This information will be updated as new experiments are conducted*  


# BCI R01 Alzheimer's Disease Supplement

Results from this study are published in the [following article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9228283/).

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
> Notes: Custom uncommitted modifications made in-line for power spectral density elements in feedback calibration, including additional notch filters for 60-Hz alias and harmonic artifact selectable character set that will include/exclude < and _ as desired for older participants Online computation of relative PSD in feedback calibration will utilize only the filtered spectrum in the denominator (e.g., 2-45 Hz or 7-20 Hz, in most cases), rather than a filtered version of the entire visible spectrum (e.g., 0-150 Hz after downsampling a VR300 recording by a factor of 2).  Number of commits: 4. Unique commit identifiers: e9a37f8 (Aug - Sept, 2019) 68c00f8 (Sept - Nov. 2019) c9f7a3f (Nov - Dec. 2019) f2ff6d0 (Jan - Mar 2020)

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

#### Raw data file types
.csv, .txt, .log, .xlxs

#### Potential considerations/limitations
* copy phrase was discontinued after two incorrect selections
feedback was delivered by electrode with best signal quality and visually identifiable posterior alpha (varied by participant; typically P4 or Pz)
* Feedback cutoffs were modified actively throughout intervention. Specifically, week 1 values were taken after aggregating all useable baseline data. Each subsequent week, cutoffs were updated to reflect data from the previous week of intervention (e.g., week 3 cutoffs are estimated from week 2 data).
* data collection was discontinued at end of baseline for 2 participants and treatment/intervention for 1 participant given COVID policies
