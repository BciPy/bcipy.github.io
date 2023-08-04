---
layout: post
title: BciPy Hardware and OS Configuration
categories: [BciPy Documentation]
tags: [featured, bci, brain computer interface, hardware, os, configuration, macos, windows, linux, usage, ram, cpu, gpu, graphics card, usb, laptop, desktop, system, disable, power, performance, network, connection, wifi, bluetooth, background, cortana, battery]
author: [Tab Memmott]

---

#### Sections
{:.no_toc}
* TOC
{:toc}

# BciPy Hardware and OS Configuration
-------------------------------------

There are several configuration and hardware requirements that must be met in order to use BciPy for data collection and meet the timing requirements needed for ERP studies. These requirements are listed below.

## General Requirements

### Hardware

A computer with the following hardware is required to run BciPy for data collection. These requirements are based on the timing requirements for ERP studies. A commercial gaming laptop or desktop will meet these requirements, but note the system configuration requirements below.

*note*: Less capable hardware may work, but is not guaranteed. More capable hardware may be required for more complex custom built tasks.

- 12GB DDR4 RAM
- 2.3Hz, 8-core CPU (Intel i7 or better)
- 2GB dedicated graphics card (Nvidia GTX 1050 or better)
- 1GB free disk space
- 2 USB (3.0) ports (for EEG and other devices) *note*: Bluetooth devices are not supported at this time. While collection works, timing via LSL has not tested well in the past. Proceed with caution and do timing tests before using in an ERP study.

### System

- Remove all unnecessary applications
- Disable all power saving features (e.g. sleep, hibernate, etc.)
- Set to performance mode
- Using the graphics card control panel ensure that the graphics card is set to the required card (>= 2GB of dedicated GPU memory) 
- Disable all automatic 
    - updates
    - virus scans
    - cloud sync
    - file indexing
    - file compression
    - backups
    - notifications
    - etc.
- Disable all network connections (e.g. wifi, bluetooth, etc.)
- Disable all background applications (e.g. chat, email, etc.)
- Disable all background listening processes (e.g. Cortana, etc.)
- Ensure if using a laptop that it is plugged in and charging, and that the battery is set to performance mode. This is critical in some laptop architectures, due to the second onboard graphics card that is used to save power and will not be sufficient for ERP presentations.

## OS Specific Requirements

*note*: BciPy is designed to install on most modern operating systems. However, there are some additional requirements for each operating system that must be met before installation can be completed. In addition, many devices will only release drivers for Windows, so it is recommended to use Windows for data collection unless you know that your device is supported on another operating system or can provide your own drivers.

### Linux

Ubuntu 22.04 is the recommended operating system for BciPy. Other versions may work, however they are not tested for support. Additional libraries will need to be installed and can be found in the `scripts\shell\linux_requirements.sh` file in the BciPy repository.

### Windows

Windows 11 is the recommended operating system for BciPy. Windows 10 is also supported. Windows 7 is no longer tested for support, however older version may work. A pro version of Windows is required to disable all automatic features including updates and Cortana. It is recommended to enable data encryption on the drive to protect participant data using BitLocker.

- Windows 10 Pro 64-bit
- Windows 11 Pro 64-bit

### Mac

MacOS Big Sur is the recommended operating system for BciPy. Other versions will likely work, however they are not tested for support. XCode and command line tools are required to install BciPy. `xcode-select --install`. See the FAQ section for additional M1 chip support information.
