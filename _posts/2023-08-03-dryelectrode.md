---
layout: post
title: Dry Electrode Procedures
categories: [Clinical Documentation]
tags: [featured, DSI, Wearable Sensing, VR300, DSI 24]
author: [Dan Klee]

---

#### Sections
{:.no_toc}
* TOC
{:toc}

# Set up & procedures
This section contains information on set up for specific equipment that may have been learned by clinical team through experiments. This does not contain very general information for such equipment that can be contained in a manual.

## Wearable Sensing VR300

Product page for [VR300](https://wearablesensing.com/vr300/)

Refer to manual for general set up instructions!

### Signal quality issues with cap
* The VR300 is a sparse-array dry-electrode one-size-fits-all cap with linked-ear reference/ground (clips). The primary difficulty observed by the clinical team with application of the VR300 has been difficulty fitting the cap on persons with particularly small/large or oblong-shaped heads. F7 and FCz electrodes are relatively free-floating, but the Pz/P4/PO7/PO8/Oz complex is rigidly fixed to a single plastic lattice at the back of the unit. If any of these electrodes are "floating", then they will be more susceptible to ambient electrical noise, EMG, etc. Posterior electrodes in particular will record neck EMG if a participant is sitting in a strained position and electrode contact(s) is/are bad.
* Because the shape/fit of the cap is static and does not always work well for certain head shapes, pressure differences cause a plethora of issues. Cardioballistic artifact (CBA; visible heart beat) will appear if an electrode is pressed too tightly against a blood vessel.

### Troubleshooting signal quality issues
* Make sure ear clips are properly attached to earlobes. The more surface area each clip touches, the better the signal. Clean earlobes with alcohol or water and let dry, if needed.
* Fitting is a primary concern for this unit. Set the cap as far forward as you can when fitting (front strap edge should sit 1-2 cm above eyebrow ridge), but make sure you can observe contact with Pz and the scalp. If Pz is "floating" above the hair/skin, push the cap down and slide back only as much as necessary to get good contact with Pz.
* When first placing cap, electrodes will be "turned" to shift hair and establish skin contact. After an initial 1-2 passes of turning electrodes, focus instead on applying pressure to electrodes. Holding pressure for as long as 1 minute is sometimes necessary. Only turn electrodes as necessary (i.e., pressure is still not helping the signal).

### Special considerations for cap
* The shape of the unit sometimes applies too little pressure to the posterior sites, but also sometimes applies too much pressure to FCz/F7, causing discomfort. Make sure to monitor these sites as such and also brush hair away from the forehead under F7, as needed.
* The bulky shell of the VR300 makes alignment difficult. When fitting the cap, do your best to put the unit on straight, then stand ~5-6 feet in front of the participant and ask them to look straight ahead and lower their chin to their chest (if able). Visually confirm alignment of the midline electrodes (i.e., FCz and Pz).
* Our version of the cap utilizes a modified montage in the DSI Streamer software (where we check signal quality before initiating BciPy testing; a montage is just a list of electrodes w/ placement info). Sometimes you might notice a difference in how the signal looks via the DSI streamer when compared to the BciPy EEG viewer. This variance is possibly related to the referencing mechanisms involved in either display. The DSI streamer montage from Wearable currently designates P4 as the common reference for all scalp electrodes. Our BciPy system uses the linked-ear clips as a reference instead. As such, make sure in particular that the signals look good for A1/2 and P4 in the Wearable DSI streamer before moving to BciPy (ideally everything will look good in both, but this item is particularly important).

## Wearable Sensing DSI-24

Product page for [DSI-24](https://wearablesensing.com/dsi-24/)

Refer to manual for general set up instructions!

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
