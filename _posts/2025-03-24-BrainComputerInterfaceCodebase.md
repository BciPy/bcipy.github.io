---
layout: post
title: BciPy Introduction and Setup
categories: [BciPy Documentation]
tags: featured, bci, brain-computer interface, intro, introduction, install, installation, setup, dependencies, python, pip, requirements, requirements-dev, macos, windows, linux, usage
author: [Tab Memmott]

---
#### Sections
{:.no_toc}
* TOC
{:toc}

# BciPy

BciPy is a library for conducting Brain-Computer Interface experiments in Python. It functions as a standalone application for experimental data collection or you can take the tools you need and start coding your own system. See our official BciPy documentation including affiliations and more context information [here](https://bcipy.github.io/).

It will run on the latest windows (10, 11), linux (ubuntu 22.04) and macos (Sonoma). Other versions may work as well, but are not guaranteed. To see supported versions and operating systems as of this release see here: [BciPy Builds](https://github.com/CAMBI-tech/BciPy/actions/workflows/main.yml).

*Please cite us when using!*

```text
Memmott, T., Koçanaoğulları, A., Lawhead, M., Klee, D., Dudy, S., Fried-Oken, M., & Oken, B. (2021). BciPy: brain–computer interface software in Python. Brain-Computer Interfaces, 1-18.
```

## Dependencies

This project requires Python 3.9 or 3.10. Please see notes below for additional OS specific dependencies before installation can be completed and reference our documentation/FAQs for more information: <https://bcipy.github.io/hardware-os-config/>

### Linux

You will need to install the prerequisites defined in `scripts\shell\linux_requirements.sh` as well as `pip install attrdict3`.

### Windows

If you are using a Windows machine, you will need to install the [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).

### Mac

If you are using a Mac, you will need to install XCode and enable command line tools. `xcode-select --install`. If using an m1/2 chip, you will need to use the install script in `scripts/shell/m2chip_install.sh` to install the prerequisites. You may also need to use the Rosetta terminal to run the install script, but this has not been necessary in our testing using m2 chips.

If using zsh, instead of bash, you may encounter a segementation fault when running BciPy. This is due to an issue in a dependeancy of psychopy with no known fix as of yet. Please use bash instead of zsh for now.

## Installation

### BciPy Setup

In order to run BciPy on your computer, after following the dependencies above, you will need to install the BciPy package.

To install for use locally and use of the GUI:

1. Git clone <https://github.com/BciPy/BciPy.git>.
2. Change directory in your terminal to the repo directory.
3. Install BciPy `pip install .` This will install the package and all dependencies. Ensure after making changes to the code, you run `pip install .` again to update the package.

If wanting the latest version from PyPi and to build using modules:

1. `pip install bcipy`

Alternately, if [Make](http://www.mingw.org/) is installed, you may run the follow command to install:

```sh
# install in development mode
make dev-install
```

### Client Usage

#### Run an experiment protocol or task

Invoke an experiment protocol or task directly using command line utility `bcipy`.

Use the help flag to see other available input options: `bcipy --help`

You can pass it attributes with flags, if desired.

* Run with a User ID and Task:
  * `bcipy --user "bci_user" --task "RSVP Calibration"`
* Run with a User ID and Tasks with a registered Protocol:
  * `bcipy --user "bci_user" --experiment "default"`
* Run with fake data:
  * `bcipy --fake`
* Run without visualizations:
  * `bcipy --noviz`
* Run with alerts after each Task execution:
  * `bcipy --alert`
* Run with custom parameters:
  * `bcipy --parameters "path/to/valid/parameters.json"`
  
#### Train a signal model with registered BciPy models

To train a signal model (currently `PCARDAKDE` and `GazeModels`), run the following command after installing BciPy:

`bcipy-train`

Use the help flag to see other available input options: `bcipy-train --help`
  
#### Visualize ERP data from a session with Target / Non-Target labels

To generate plots that can be shown or saved after collection of data, run the following command after installing BciPy:

`bcipy-erp-viz`

Use the help flag to see other available input options: `bcipy-erp-viz --help`

#### BciPy Simulator Usage

The simulator can be run using the command line utility `bcipy-sim`.

To run the simulator with a single data folder, a custom parameters file, a trained model, and 5 iterations, use the following command:

`bcipy-sim -d my_data_folder/ -p my_parameters.json -m my_models/ -n 5`

For more information or to see other available input options, use the help flag: `bcipy-sim --help`. In addition, more information can be found in the simulator module README.

### Package Usage

```python
from bcipy.helpers import system_utils
system_utils.get_system_info()
```

### GUI Usage

Run the following command in your terminal to start the BciPy GUI:

```sh
python bcipy/gui/BCInterface.py
```

Alternately, if Make is installed, you may run the follow command to start the GUI from the BciPy root directory:

```sh
make bci-gui
```

## Core Modules

This a list of the major modules and their functionality. Each module will contain its own README, demo and tests. Please check them out for more information!

* `acquisition`: acquires data, gives back desired time series, saves to file at end of session.
* `config`: configuration parameters for the application, including paths and data filenames.
* `core`: core data structures and methods needed for BciPy operation. These include triggers, parameters, and raw data.
* `display`: handles display of stimuli on screen and passes back stimuli timing.
* `feedback`: feedback mechanisms for sound and visual stimuli.
* `gui`: end-user interface into registered bci tasks and parameter editing. See BCInterface.py.
* `helpers`: helpful functions needed for interactions between modules and general utility.
* `io`: load, save, and convert data files. Ex. BIDS, BrainVision, EDF, MNE, CSV, JSON, etc.
* `language`: gives probabilities of next symbols during typing.
* `main`: executor of experiments. Main entry point into the application
* `parameters`: location of json parameters. This includes parameters.json (main experiment / app configuration) and device.json (device registry and configuration).
* `signal`: eeg signal models, gaze signal models, filters, processing, evaluators and viewers.
* `simulator`: provides support for running simulations based off of previously collected data.
* `static`: image and sound stimuli, misc manuals, and readable texts for gui.
* `task`: bcipy implemented user tasks. Main collection of bci modules for use during various experimentation. Ex. RSVP Calibration.

## Paradigms

See `bcipy/task/README.md` for more information on all supported paradigms, tasks, actions and modes. The following are the supported and validated paradigms:

### RSVPKeyboard

*RSVP KeyboardTM* is an EEG (electroencephalography) based BCI (brain computer interface) typing system. It utilizes a visual presentation technique called rapid serial visual presentation (RSVP). In RSVP, the options are presented rapidly at a single location with a temporal separation. Similarly in RSVP KeyboardTM, the symbols (the letters and additional symbols) are shown at the center of screen. When the subject wants to select a symbol, they await the intended symbol during the presentation and elicit a p300 response to a target symbol.

References:

```text
Orhan, U., Hild, K. E., 2nd, Erdogmus, D., Roark, B., Oken, B., & Fried-Oken, M. (2012). RSVP Keyboard: An EEG Based Typing Interface. Proceedings of the ... IEEE International Conference on Acoustics, Speech, and Signal Processing. ICASSP (Conference), 10.1109/ICASSP.2012.6287966. https://doi.org/10.1109/ICASSP.2012.6287966
```

### Matrix Speller

Matrix Speller is an EEG (electroencephalography) based BCI (brain computer interface) typing system. It utilizes a visual presentation technique called Single Character Presentation (SCP). In matrix speller, the symbols are arranged in a matrix with fixed number of rows and columns. Using SCP, subsets of these symbols are intensified (i.e. highlighted) usually in pseudorandom order to produce an odd ball paradigm to induce p300 responses.

References:

```text
Farwell, L. A., & Donchin, E. (1988). Talking off the top of your head: toward a mental prosthesis utilizing event-related brain potentials. Electroencephalography and clinical Neurophysiology, 70(6), 510-523.

Ahani A, Moghadamfalahi M, Erdogmus D. Language-Model Assisted And Icon-based Communication Through a Brain Computer Interface With Different Presentation Paradigms. IEEE Trans Neural Syst Rehabil Eng. 2018 Jul 25. doi: 10.1109/TNSRE.2018.2859432.
```

## Demo

All major functions and modules have demo and test files associated with them which may be run locally. This should help orient you to the functionality as well as serve as documentation. *If you add to the repo, you should be adding tests and fixing any test that fail when you change the code.*

For example, you may run the main BciPy demo by:

`python demo/bci_main_demo.py`

This demo will load in parameters and execute a demo task defined in the file. There are demo files contained in most modules, excepting gui, signal and parameters. Run them as a python script!

## Offset Determination and Correction

Static offset determination and correction are critical steps before starting an experiment. BciPy uses LSL to acquire EEG data and Psychopy to present stimuli. The synchronization between the two systems is crucial for accurate data collection and analysis.

[LSL synchronization documentation](https://labstreaminglayer.readthedocs.io/info/time_synchronization.html)
[PsychoPy timing documentation](https://www.psychopy.org/general/timing/index.html)

A static offset is the regular time difference between our signals and stimuli. This offset is determined through testing via a photodiode or other triggering mechanism. The offset correction is done by shifting the EEG signal by the determined offset using the `static_offset` parameter.

After running a timing verification task (such as, RSVPTimingVerification) with a photodiode attached to the display and connected to a device, the offset can be determined by analyzing the data. Use the `offset` module to recommend an offset correction value and display the results.

To run the offset determination and print the results, use the following command:

```bash
python bcipy/helpers/offset.py -r
```

After running the above command, the recommended offset correction value will be displayed in the terminal and can be passed to determine system stability and display the results.

```bash
# Let's say the recommneded offset value is 0.1
python bcipy/helpers/offset.py --offset "0.1" -p
```

Alternately, if Make is installed, you may run the follow command to run offset determination and display the results:

```sh
make offset-recommend
```
