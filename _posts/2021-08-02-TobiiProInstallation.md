---
layout: post
title: App-TobiiPro Installation
categories: [BciPy Documentation]
author: Matthew Lawhead (OHSU)

---

#### Sections in this article
{:.no_toc}
* TOC
{:toc}

# App-TobiiPro Installation

This document provides detailed instructions for building the [LabStreamingLayer TobiiPro](https://github.com/labstreaminglayer/App-TobiiPro) application from source for interfacing with Tobii eye trackers.

[https://labstreaminglayer.readthedocs.io/dev/app_build.html](https://labstreaminglayer.readthedocs.io/dev/app_build.html)
[https://labstreaminglayer.readthedocs.io/dev/build_env.html](https://labstreaminglayer.readthedocs.io/dev/build_env.html)


## Clone repository

- Original: [https://github.com/labstreaminglayer/App-TobiiPro](https://github.com/labstreaminglayer/App-TobiiPro)
- Fork: [https://github.com/CAMBI-tech/App-TobiiPro](https://github.com/CAMBI-tech/App-TobiiPro)


## Download / Install Dependencies:

The TobiiPro LSL app has three main dependencies:

- TobiiPro C SDK
- LSL
- Qt5

### TobiiPro C SDK

The TobiiPro C SDK is what the app uses to interface with the device. The cmake build looks for this in a specific location within the source code.

- Download the [TobiiPro C SDK](https://www.tobiipro.com/product-listing/tobii-pro-sdk/#Download)
- Extract the SDK and copy the '/64' directory (which has the /include and /lib folders) into the App-TobiiPro directory and rename to 'tobii'


### LSL

- Download latest release of [LabStreamingLayer](https://github.com/sccn/liblsl/releases)
- Extract it to a known location (this can be configured with cmake).

### Qt

The TobiiPro app currently requires Qt5. This can be installed using a package manager, such as homebrew, or manually using the Qt Installer. To use the installer:

- Download the [Qt Installer](https://www.qt.io/download-qt-installer) (for Open Source projects).
- Create an account (login.qt.io); this is required during installation.
- Run the Qt installer and do a Custom Installation to install Qt5 (currently at 5.15.2) prebuilt components for your system. The installation location can be configured with cmake.


## Install Developer Tools

You will need a C / C++ compiler for your system, as well as the cmake build system.

- C/C++ compiler
    - Mac: XCode developer tools
    - Windows: Visual Studio
- [cmake](https://cmake.org)
    - usually installed with C tooling, but can be downloaded and installed separately

- [Visual Studio Code](https://code.visualstudio.com) is recommended for configuring and running cmake. The instructions provided are cross-platform. In addition to the IDE, you should install the [C/C++ extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack) from Microsoft, which includes the ms-vscode.cmake-tools extension.


## Configuring and Running CMake using VS Code

Building an executable with CMake is a two step process:

1. Running CMake to Configure the project and generate a native build system.
2. Call the generated build system to actually compile/link the project.

### CMake Configuration

The CMake Configuration step must run prior to generating the build. For the Configuration step, you will need to instruct cmake which compiler (kit) to use, what kind of build to generate (Release or Debug), and where it should look for dependencies.

#### Open the Project in VS Code

Open the TobiiPro source code with Visual Studio Code. Note that the various CMake commands may be automatically run by VS Code and any errors will be captured in the Output section.

#### Select a compiler

Run the `CMake: Select Kit` command to select a compiler if one has not already been selected. This will present a pulldown list of options. Note that this command may be auto-run when you open the project in VS Code. If there are no items in the list, you may need to install a C/C++ compiler (see above).


#### Select a Variant

Run the `CMake: Select Variant` command and set this to 'Release'. By default this is set to 'Debug'.

#### Add dependency locations

Cmake needs to know where to look for the installed dependencies used in this project. There are many ways to provide cmake with these paths but the simplest is to point it to the `<project>Config.cmake` file for each dependency.

In the VS Code Settings for the current Workspace, configure the `cmake.configureArgs` with the parameters:
  - `-DLSL_DIR=<path to LSL>/lib/cmake/LSL`
  - `-DQt5_DIR=<path to Qt>/lib/cmake/Qt5`

These are passed as command line arguments so the `-D` prefix is required. The `LSL_DIR` argument should be the path to the directory with the `LSLConfig.cmake` file, and the `Qt5_DIR` should be the path to the `Qt5Config.make` file.

Alternatively, these can be provided by using a `settings.json` file in the `.vscode` directory with the contents:

    {
        "cmake.configureArgs": [
            "-DLSL_DIR=<path_to_LSL>/lib/cmake/LSL",
            "-DQt5_DIR<path>/5.15.2/clang_64/lib/cmake/Qt5"
        ]
    }

See also:
- [CMake Using Dependencies Guide](https://cmake.org/cmake/help/latest/guide/using-dependencies/index.html#guide:Using%20Dependencies%20Guide)
- [CMake find_package documentation](https://cmake.org/cmake/help/latest/command/find_package.html#command:find_package)


#### Add Support for Compiling C

The LSL cmake file executes C code to determine the system architecture. Without modification, attempting to run cmake will result in an error that the C language is not enabled. There are two ways to resolve this:

1. _[preferred method]_ Add `enable_language(C)` in the liblsl `LSLCMake.cmake` (immediately before the `try_compile`). See [github issues](https://github.com/labstreaminglayer/App-TobiiPro/issues/5).

2. Modify the TobiiPro `CMakeLists.txt` file to include support for compiling C as well as C++ code.

Change:

    project(TobiiPro
    	LANGUAGES CXX
    	VERSION 1.13.0)

To:

    project(TobiiPro
    	LANGUAGES C CXX
    	VERSION 1.13.0)


#### Run CMake Configure

The `CMake: Configure` command generates the build files in the project's build folder. These files will be written to the `/build` folder (unless it is configured differently).

The Output browser will show the command issued and will provide feedback (for missing dependencies, etc).


### CMake Build

Run the `CMake: Build` command to build the final executable. This will be located in the `/build` directory and called `TobiiPro`.

