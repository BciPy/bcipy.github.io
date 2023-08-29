---
title: How to Install BciPy on Mac M1 Chip 
---

If you are using a computer with the Mac M1 chip, you may run into issues with installing some packages of BciPy including psychopy and pyqt5. 

The best workaround for this is to use the Rosetta 2 Terminal, which emulates an i386 architecture instead of arm64.

## To create a Rosetta Terminal: 
1. Open finder and naviagate into applications. Locate the Terminal app

2. Right click on the terminal app and click "Get info". From the "Get info" menu, check the box that says "Open using Rosetta".

3. Force quit the terminal application and reopen a new terminal window.

Verify you're in the rosetta terminal by running `arch` command (should see `i386`). Only use the Rosetta Terminal for all the following steps/any usage of BciPy. You can configure your IDE to use rosetta terminal too through some googling.


## To Install BciPy (within the Rosetta Terminal)

Pre-requisite: install [brew](https://docs.brew.sh/Installation)

1. Git clone https://github.com/BciPy/BciPy.git. Check in to the most up to date branch.

2. Run the following command in your terminal:
    > `arch -arm64 brew install python@3.9`

    Reinstall If you already had python 3.9
    > `arch -arm64 brew reinstall python@3.9`

3. Create a virtual environment using python 3.9:
    > `python3 -m venv --system-site-packages venv`
4. Open the virtual environment:
    > `source venv/bin/activate`

5. Edit the following lines in `requirements.txt` accordingly
- pylsl==1.14.0 --> pylsl==1.15.0
- pyedflib==0.1.30 --> pyedflib
- PyQt5==5.15.1 --> pyqt5

6. Globally installing pyqt5 
    > `arch -arm64 brew install pyqt@5`

7. Run the following command in your terminal (make sure that your pip is up to date if there are any issues at this step):
    > `pip install -r requirements.txt`

    > `pip install -r dev_requirements.txt`

    > `pip install -e .` 

8. Install XCode and enable command line tools:
    > `xcode-select --install`
9. To install the M1 compatible version of PsychoPy, run:
    > `pip install Psychopy==2023.1.0 --install-option="--no-deps"`


You can open and use the Rosetta terminal within different IDEs. You just have to make sure that you add it in the settings and then switch to it before you try to run BciPy scripts. The correct packages are only installed in the Rosetta Terminal, so BciPy will not work in zsh/bash, etc. 