---
layout: post
title: BciPy Data Handling
categories: [BciPy Documentation]
tags: featured, bci, brain-computer interface, intro, introduction, data, python, usage
author: [Tab Memmott]

---
#### Sections
{:.no_toc}
* TOC
{:toc}

# Handling BciPy Data

This document provides an overview of the BciPy data handling process, including how to load, process, and manage data in two primary modes: Calibration and Copy Phrase.

This document outlines the general principles of handling data within the BciPy framework. Specific implementations and code examples for using the TriggerHandler and RawData classes, as well as for running various data tasks, can be found in the corresponding sections of the BciPy documentation or source code.

## Data Modes

There are two primary modes in BciPy with different data structures and purposes: Calibration and Copy Phrase.

### Calibration Mode

Data in Calibration mode contains triggers and raw data.

Calibration mode is typically used for initial data collection where the system is calibrated to the user's brain signals.
The data collected in this mode may include EEG signals, stimulus triggers, and other raw data for system calibration. The data is typically used to train machine learning models or to analyze the user's brain signals for further processing.

### Copy Phrase Mode

Data in Copy Phrase mode contains additional session information. This mode includes all data from Calibration mode plus session metadata like:

* Model Evidence: Information about model accuracy or performance.
* Selection Metrics: Metrics regarding task selection (e.g., which tasks were selected, or the difficulty of the tasks).
* Typing Metrics: Information related to typing performance (e.g., speed, accuracy).

The data is more comprehensive in this mode, as it also includes session-related metrics and other experiment-related information.

## Data Organization and File Structure

BciPy data is saved in a hierarchical file structure designed to keep data organized by user, date, experiment, run, and task. The basic directory structure looks as follows:

```text
data_save_location/
    user_id/
        date/
            experiment_id/
                run_id <datetimestamp>/
                    task_id/
                        logs/
                            task_log_data
                        task_data (e.g. acquisition data, parameters, visualizations)
                    task_id/
                        logs/
                            task_log_data
                        task_data (e.g. acquisition data, parameters, visualizations)
                    logs/
                        protocol_log_data
                    protocol_data (system data, protocol/tasks executed)
```

### Directory Breakdown

* `user_id/`: A directory for a specific user that is typically identified by a unique user identifier.
* `date/`: Subdirectory containing data for a specific session date.
* `experiment_id/`: Subdirectory containing data for a specific experiment run.
* `run_id/`: A subdirectory uniquely identifying a run by its timestamp (e.g., run_2025-01-03_11-35-22/).
* `task_id/`: Contains task-specific data, typically for different phases of the experiment (e.g., calibration, copy phrase, etc.).
* `logs/`: Contains log files for task-specific logs (task_log_data).
* `task_data/`: Contains the task-specific data files (e.g., acquisition data, parameters, and visualizations).
* `logs/`: A separate directory containing protocol logs. These logs typically contain information about system-level activities and task executions.
* `protocol_data`: This holds system data such as protocol/task execution logs (e.g., which tasks were executed, protocol information).

## Data Loading

Regardless of the mode (Calibration or Copy Phrase), BciPy uses the following classes to load the raw data:

### Triggers and TriggerHandler

The Trigger and TriggerHandler classes are essential for identifying and extracting trigger events from the raw data, which are used to segment the data into different task phases or events. The TriggerHandler class is used to load trigger data from the saved experiment files and ensure that the triggers are correctly imported into the BciPy framework for further use. This documentation will cover the basics and how to load data, as well as the different trigger types and their usage. If wanting to implement a new task, it is recommended to use the TriggerHandler class to manage triggers for writing. Please consult the source code for more information.

### Triggers

Triggers consist of a label, type and a timestamp. These are what is used to align events both in real-time and after a session for further processing or model training. During operation of a BciPy task, Triggers are generated when display or other events of interest occur. These are timestamped using a monotonic clock (See helpers/clock.py).

A new Trigger may defined as follows:

```python
from bcipy.core.triggers import Trigger, TriggerType

# label can be any utf-8 compliant string
nontarget_trigger = Trigger('nontarget_label', TriggerType.NONTARGET, 1.0111)
```

### Trigger Types

The supported internal trigger types are as follows:

```python
NONTARGET = "nontarget"
TARGET = "target"
FIXATION = "fixation"
PROMPT = "prompt"
SYSTEM = "system"
OFFSET = "offset"
EVENT = "event"
PREVIEW = "preview"
```

### Trigger Handler Loading

To load a BciPy triggers.txt file, the TriggerHandler load method can be used. Because it is a staticmethod, the class does not need to be initialized before the load method is used.

```python
from bcipy.core.triggers import TriggerHandler

path_to_trigger_save_location = './triggers.txt'

triggers = TriggerHandler.load(path_to_trigger_save_location)
# it will load in data like this:
# [Trigger: label=[starting_offset] type=[offset] time=[-13149613.488788936], Trigger: label=[x] type=[prompt] time=[4.96745322458446]]
```

Alternately, you can pass offset and exclusion as keyword arguments to modify the behavior of `TriggerHandler.load`. Offset will add time to every timestamp loaded. Use this to correct any static system offsets! The default value for offset is 0.0. Exclusions can be used to pre-filter any unwanted Triggers, such as SYSTEM.

```python
from bcipy.core.triggers import TriggerHandler

path_to_trigger_save_location = './triggers.txt'

# exclude system triggers
triggers = TriggerHandler.load(path_to_trigger_save_location, exclusion=[TriggerType.SYSTEM])

# apply a 2 second offset to all timestamps loaded
triggers = TriggerHandler.load(path_to_trigger_save_location, offset=2.0)
```

### Trigger Decoder

Most may find using the trigger decoder to be the easiest for loading their triggers. This will load in the triggers and apply any offsets or exclusions as needed. The trigger decoder will also return the triggers in a dictionary format, which can be useful for further processing.

```python
from bcipy.core.triggers import trigger_decoder, TriggerType

data_folder = 'path/to/data'
TRIGGER_FILENAME = 'triggers.txt'
static_offset = 0.1 # common offset for EEG data in BciPy
device_type = 'EEG'

trigger_targetness, trigger_timing, trigger_labels = trigger_decoder(
        trigger_path=f"{data_folder}/{TRIGGER_FILENAME}",
        exclusion=[TriggerType.PREVIEW, TriggerType.EVENT],
        offset=static_offset,
        remove_pre_fixation=True,
        device_type=device_type
    )
```

### RawData

The RawData class is used to load the raw signal data (e.g., EEG, ECG, or other biosignals) from experiment runs. Raw data is in time-series format and may need to be pre-processed (e.g., filtered) before being used for analysis or model training.

The RawData class provides methods to load raw data (.csv) and allows users to specify which channels and data segments to include for further analysis.

```python
from bcipy.io.load import load_raw_data

# Load raw data from a file
raw_data = load_raw_data('path/to/raw_data_file.csv')

# Extract relevant information from the raw data
channels = raw_data.channels
type_amp = raw_data.daq_type
sample_rate = raw_data.sample_rate
data, fs = raw_data.by_channel()
```

Under the hood this method uses the `RawData` class to load the data.

### Parameters

The `load_json_parameters` method can be used to load parameters from a JSON file. This method is used to load the parameters file saved with the data. The parameters file contains information about the experiment, such as the task window, prestimulus length, trials per inquiry, and other task-specific parameters.

```python
from bcipy.io.load import load_json_parameters

# Load parameters from a JSON file, the value_cast parameter is used to cast the values to the correct type (e.g., int, float, etc.)
parameters = load_json_parameters('path/to/parameters.json', value_cast=True)
```

In addition, there may be some information saved in the devices.json file that can be loaded using the `load` method from the `bcipy.acquisition.devices` module.

```python
import bcipy.acquisition.devices as devices

daq_type = 'DSI-24' # this can also be extracted from the RawData object via raw_data.daq_type
devices.load('path/to/devices.json')
device_spec = devices.preconfigured_device(daq_type)
static_offset = device_spec.static_offset # pull the static offset from the device spec
channels = device_spec.channels # pull the channels from the device spec
labels = device_spec.labels # pull the labels from the device spec
```

## Data Processing and Usage

Once data is loaded, it can be processed in various ways depending on the task at hand. Below are the common use cases for data handling in BciPy.

### Filtering RawData

The raw data can be filtered based on specific requirements (e.g., frequency ranges, events of interest).
Filtering can be performed using the `get_default_transform` method, which allows users to specify a transform that can be applied to the raw data.

```python
from bcipy.signal.process import get_default_transform

sample_rate = 256
notch_filter_frequency = 60
filter_low = 2
filter_high = 45
filter_order = 2
down_sampling_rate = 2

default_transform = get_default_transform(
        sample_rate_hz=sample_rate,
        notch_freq_hz=notch_filter_frequency,
        bandpass_low=filter_low,
        bandpass_high=filter_high,
        bandpass_order=filter_order,
        downsample_factor=down_sampling_rate,
    )

# use any of the get data methods on RawData to apply the transform. This will return the transformed data and new sample rate.
data, fs = data.by_channel(transform=default_transform)
```

### Filtering using MNE

MNE is a powerful Python library for processing EEG data. It provides a wide range of functions for filtering, transforming, and visualizing EEG data. BciPy leverages MNE for many of its data processing and visualization tasks and supports converting RawData objects to MNE Raw objects for further processing.

```python
from bcipy.io.convert import convert_to_mne

# Convert RawData to MNE Raw object. This method also allows for a channel map and transform to be passed in.
raw_mne = convert_to_mne(raw_data)

filter_low = 2
filter_high = 45
# Apply filtering using MNE
raw_mne.filter(l_freq=filter_low, h_freq=filter_high)

# Plot the raw data
raw_mne.plot()
```

#### Adding triggers to MNE Raw object

```python
from bcipy.io.convert import convert_to_mne
from bcipy.core.stimuli import mne_epochs
from bcipy.core.triggers import trigger_decoder, TriggerType

# Many of these can be loaded from the BciPy parameters files saved with the data.
data_folder = 'path/to/data'
TRIGGER_FILENAME = 'triggers.txt'
static_offset = 0.1 # common offset for EEG data in BciPy.
device_type = 'EEG'
trial_length = 0.8 # trial length in seconds

# Load trigger data
trigger_targetness, trigger_timing, trigger_labels = trigger_decoder(
        trigger_path=f"{data_folder}/{TRIGGER_FILENAME}",
        exclusion=[TriggerType.PREVIEW, TriggerType.EVENT],
        offset=static_offset,
        remove_pre_fixation=True,
        device_type=device_type
    )

# Using the raw_mne loaded from the convert_to_mne function (see above using raw_mne = convert_to_mne(raw_data))
# Depending on the analysis, a channel map should be used to remove any non-EEG channels
# The trigger timing and labels are used to create epochs, remove any unwanted triggers, and create an MNE Epochs object.
epochs = mne_epochs(raw_mne, trial_length, trigger_timing, trigger_labels)

# Plot the epochs
epochs.plot()

# Average the epochs and plot the evoked response
evoked = epochs['1'].average()
evoked.plot()
evoked.plot_topomap(times=[0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7])
```

### Training Models

In both Calibration and Copy Phrase modes, the loaded data can be used to train machine learning models. Typically, the data is split into training and testing sets, with triggers and raw signal data being used to extract features and labels.

Model training may involve signal processing techniques like feature extraction (e.g., frequency band power, coherence, etc.) and applying algorithms like SVM, Random Forest, or Neural Networks. BciPy provides a range of tools and utilities for training and evaluating machine learning models on EEG data. 

See the `bcipy.signal.model` module for more information. In particular, the `bcipy.signal.model.offline_analysis` module provides examples of how to train and evaluate models on EEG data.

### Converting Data to BIDS Format

For sharing data with other researchers, BciPy supports converting data to the BIDS (Brain Imaging Data Structure) format. BIDS is a standardized format for sharing and organizing neuroimaging data, which is particularly useful when integrating EEG or other neurophysiological data with imaging data. The conversion process typically involves organizing the data into the BIDS directory structure and populating the required metadata files (e.g., dataset_description.json, eeg.json, etc.).


BciPy provides tools for converting data to the BIDS format, which can be found in the `bcipy.io.convert` module. There is a demo script in the `bcipy.io.demo.demo_convert.py` module that demonstrates how to convert BciPy data to the BIDS format.

## Putting it all together

The BciPy data handling process involves loading raw data, extracting triggers, filtering the data, and processing it for further analysis or model training. The TriggerHandler and RawData classes are used to load and process data in Calibration and Copy Phrase modes. The data is organized in a hierarchical file structure, and users can filter and process the data using various methods and tools provided by BciPy. The processed data can be used for training machine learning models, analyzing EEG signals, or converting data to the BIDS format for sharing with other researchers.

Here's an example of how to put it all together to visualize ERP data:

```python

import bcipy.acquisition.devices as devices
from bcipy.config import (DEFAULT_DEVICE_SPEC_FILENAME,
                          DEFAULT_PARAMETERS_FILENAME, RAW_DATA_FILENAME,
                          TRIGGER_FILENAME)
from bcipy.helpers.acquisition import analysis_channels
from bcipy.io.load import (load_experimental_data, load_json_parameters,
                           load_raw_data)
from bcipy.core.triggers import TriggerType, trigger_decoder
from bcipy.helpers.visualization import visualize_erp
from bcipy.signal.process import get_default_transform

if __name__ == '__main__':
    import argparse
    from pathlib import Path

    parser = argparse.ArgumentParser()
    parser.add_argument(
        '-p',
        '--path',
        help='Path to the directory with raw_data to be converted',
        required=False)
    parser.add_argument("--show", dest="show", action="store_true")
    parser.add_argument("--save", dest="save", action="store_true")
    parser.set_defaults(show=False)
    parser.set_defaults(save=False)
    args = parser.parse_args()

    path = args.path
    if not path:
        path = load_experimental_data(
            message="Select the folder containing the raw_data.csv, parameters.json and triggers.txt",
            strict=True
        )

    parameters = load_json_parameters(f'{path}/{DEFAULT_PARAMETERS_FILENAME}',
                                      value_cast=True)

    # extract all relevant parameters
    trial_window = parameters.get("trial_window", (0, 0.5))
    prestim_length = parameters.get("prestim_length")
    trials_per_inquiry = parameters.get("stim_length")
    # The task buffer length defines the min time between two inquiries
    # We use half of that time here to buffer during transforms
    buffer = int(parameters.get("task_buffer_length") / 2)
    # get signal filtering information
    downsample_rate = parameters.get("down_sampling_rate")
    notch_filter = parameters.get("notch_filter_frequency")
    filter_high = parameters.get("filter_high")
    filter_low = parameters.get("filter_low")
    filter_order = parameters.get("filter_order")

    raw_data = load_raw_data(Path(path, f'{RAW_DATA_FILENAME}.csv'))
    channels = raw_data.channels
    type_amp = raw_data.daq_type
    sample_rate = raw_data.sample_rate

    devices.load(Path(path, DEFAULT_DEVICE_SPEC_FILENAME))
    device_spec = devices.preconfigured_device(raw_data.daq_type)
    static_offset = device_spec.static_offset

    # setup filtering
    default_transform = get_default_transform(
        sample_rate_hz=sample_rate,
        notch_freq_hz=notch_filter,
        bandpass_low=filter_low,
        bandpass_high=filter_high,
        bandpass_order=filter_order,
        downsample_factor=downsample_rate,
    )
    # Process triggers.txt files
    trigger_targetness, trigger_timing, trigger_symbols = trigger_decoder(
        offset=static_offset,
        trigger_path=f"{path}/{TRIGGER_FILENAME}",
        exclusion=[TriggerType.PREVIEW, TriggerType.EVENT, TriggerType.FIXATION],
    )
    labels = [0 if label == 'nontarget' else 1 for label in trigger_targetness]

    channel_map = analysis_channels(channels, device_spec)

    save_path = None if not args.save else path

    figure_handles = visualize_erp(
        raw_data,
        channel_map,
        trigger_timing,
        labels,
        trial_window,
        save_path=save_path,
        show=args.show
    )
```
