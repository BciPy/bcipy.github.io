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
-------

### What is it?

BciPy is a library for conducting Brain-Computer Interface experiments in Python. It functions as a standalone application for experimental data collection or you can take the tools you need and start coding your own system. It is designed to be modular and extensible, so you can easily add your own components and algorithms. It is also designed to be easy to use, so you can get started quickly.

It will run on the latest windows (7, 10, 11), linux (ubuntu 22.04) and macos (Big Sur). Other versions may work as well, but are not guaranteed. To see supported versions and operating systems as of this release see here: [BciPy Builds](https://github.com/CAMBI-tech/BciPy/actions/workflows/main.yml).

*Please cite us when using!*

```
Memmott, T., Koçanaoğulları, A., Lawhead, M., Klee, D., Dudy, S., Fried-Oken, M., & Oken, B. (2021). BciPy: brain–computer interface software in Python. Brain-Computer Interfaces, 1-18.
```

## Dependencies
---------------
This project requires Python 3.8 or 3.9. Please see notes below for additional OS specific dependencies before installation can be completed.

### Linux

You will need to install the prerequisites defined in `scripts\shell\linux_requirements.sh` as well as `pip install attrdict3`.

### Windows

If you are using a Windows machine, you will need to install the [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).

*python 3.9 only!*
You will need to install pyWinhook manually. See [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pywinhook) for the appropriate wheel file (`pyWinhook‑1.6.2‑cp39‑cp39‑win_amd64.whl`). Then run `pip install <path_to_wheel_file>`. We also include the 64-bit wheel file in the `.bcipy/downloads/` directory.

### Mac

If you are using a Mac, you will need to install XCode and enable command line tools. `xcode-select --install`. 

## Installation
---------------

#### BciPy Setup

In order to run BciPy on your computer, after following the dependencies above, you will need to install the BciPy package.

To install for use locally,
1. Git clone https://github.com/BciPy/BciPy.git
2. Change directory in your terminal to the repo
3. Run `pip install -e .`
4. To use the KenLMLanguageModel class, you must manually install the kenlm package. `pip install kenlm==0.1 --global-option="--max_order=12"`.


If wanting the latest version from PyPi:
1. `pip install bcipy`

Alternately, if [Make](http://www.mingw.org/) is installed, you may run the follow command to install:

```sh
# install in development mode
make dev-install
```

#### Usage Locally

Two ways to get started using BciPy for data collection:
	1. Run `python bcipy/gui/BCInterface.py` in your command prompt or terminal from from base BciPy directory. This will execute the main BCI GUI. You may also use the command `make bci-gui`. 
	2. Invoke the experiment directly using command line utility `bcipy`.
		- You can pass it attributes with flags, if desired.
				Ex. `bcipy --user "bci_user" --task "RSVP Calibration"`
		- Use the help flag to see other available input options: `bcipy --help`

##### Example usage as a package

```python
from bcipy.helpers import system_utils
system_utils.get_system_info()
```
