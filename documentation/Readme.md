# LabVIEW DAQ Application Template

## Usage

1. Install LabVIEW 2021 or later
1. Open the lvproj
1. Open Main.vi
1. Run

## Preview

![Main UI](./Main%20UI.gif)

## Configuration

- Channels
  - name
  - device
  - sensor
  - calibration
- Graph
  - plot scaled data
  - small range Y axis
  - large range Y axis
- Timing
  - software-timed intervals
  - one sample per interval
  - intervals can be repeated and sequenced
  - additional samples on-button-click while running
- Logging
  - unscaled data
  - CSV format
    - sensor count
    - starting datetime
    - sensor table with rows of calibration coefficients
    - data table with rows of unscaled data samples
  - create or overwrite log file
  - append to existing log file
  - autoname with timestamp

## Data

These snippets are from the example [Jupyter notebook](./data_log%20notebook.ipynb).

```csv
sensor count,3
datetime,2023-05-13T11:44:42.804-07:00
name,Vex,CF,X0,Units,Sensor,IO Device
sim1,1.0000,1.0000,0.0000,V,Voltage,9219
sim2,1.0000,1.0000,0.0000,mm,Voltage,9219
sim3,1.0000,1.0000,0.0000,lb,Load,9219
timestamp,sim1,sim2,sim3
2023-05-13T11:44:42.840-07:00,0.0389,1.0375,2.0370
2023-05-13T11:44:43.869-07:00,0.7953,1.7660,2.7532
2023-05-13T11:44:44.989-07:00,1.2240,2.2297,3.2119
2023-05-13T11:44:46.074-07:00,1.4414,2.5315,3.5226
2023-05-13T11:44:47.177-07:00,1.6061,2.7468,3.7610
2023-05-13T11:44:48.270-07:00,1.8084,2.8984,3.9441
2023-05-13T11:44:49.370-07:00,2.0461,3.0124,4.0889
2023-05-13T11:44:50.475-07:00,2.2388,3.1089,4.2042
2023-05-13T11:44:51.575-07:00,2.3281,3.2037,4.2968
2023-05-13T11:44:52.675-07:00,2.3516,3.3082,4.3743
2023-05-13T11:44:53.778-07:00,2.4028,3.4257,4.4433
2023-05-13T11:44:54.877-07:00,2.5328,3.5511,4.5088
```

```python
import pandas as pd

data = pd.read_csv(
    "data_log.csv",
    header=6,
    index_col="timestamp",
    parse_dates=["timestamp"],
)

print(f"shape{data.shape}")
axes = data.plot.line()
```

> ```
> data.shape(181, 3)
> ```
>
> ![data log plots](./data_log%20plots.png)

## Changelog

### Baseline

LabVIEW sample project: Continuous Measurement and Logging

- Launch LabVIEW and select Create Project. From the Create Project dialog, launch the Continuous Measurement and Logging sample project.
- NI site: https://www.ni.com/en-us/support/documentation/supplemental/21/using-a-queued-message-handler-in-labview.html
- LV wiki: https://labviewwiki.org/wiki/Design_pattern

### Changes

- Make the root container for Aquired Data.ctl a cluster
- Use typedefs in the data queues/notifiers rather than raw constants
- Add 'Exit' user-action to main UI error handler
- Add overwrite-log/append-log/timestamp-log tab control to Settings Dialog
- Switch to spreadsheet log format
- Add Diagnostics subsystem loop
- Add Interval Timer subsystem
- Add "Save Now" button and behavior
- Add Acquisition Status loop and countdown
- Add multi-channel support
- Implement data calibration
- Implement per channel null-offset
- Plot scaled data, log unscaled data
- Add axis settings to Settings Dialog
- Add log file path control to main UI
- Detect software and hardware resources on host system
- Add dynamic DAQmx API detection and use
- Add plugin selection to Settings Dialog
