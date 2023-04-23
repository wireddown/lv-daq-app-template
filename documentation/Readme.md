# LabVIEW DAQ Application Template

## Usage

1. Install LabVIEW 2021 or later
1. Open the lvproj
1. Open Main.vi
1. Run

## Preview

![Main UI](./Main%20UI.gif)

## Configuration

- Plots
  - name
  - device
  - calibration
- Timing
  - software-timed intervals
  - one sample per interval
  - intervals can be repeated and sequenced
  - additional samples on-button-click while running
- Logging
  - CSV format
    - starting datetime
    - sensor table with rows of calibration coefficients
    - data table with rows of unscaled data samples
  - create or overwrite log file
  - append to existing log file
  - autoname with timestamp

## Data

These snippets are from the example [Jupyter notebook](./data_log%20notebook.ipynb).

```csv
datetime,2023-04-23T16:26:50.791-07:00
name,Vex,CF,X0
sim1 (psi),1.0000,1.0000,0.0000
sim2 (lbs),1.0000,1.0000,0.0000
sim3 (in),1.0000,1.0000,0.0000
sim4 (in),1.0000,1.0000,0.0000
sim5 (V),1.0000,1.0000,0.0000
timestamp,sim1 (psi),sim2 (lbs),sim3 (in),sim4 (in),sim5 (V)
2023-04-23T16:26:50.826-07:00,0.0365,1.0351,2.0346,3.0344,4.0343
2023-04-23T16:26:51.841-07:00,0.7872,1.7579,2.7452,3.7386,4.7345
2023-04-23T16:26:52.941-07:00,1.2143,2.2177,3.1999,4.1883,5.1807
2023-04-23T16:26:54.042-07:00,1.4384,2.5271,3.5179,4.5053,5.4956
2023-04-23T16:26:55.140-07:00,1.6020,2.7427,3.7562,4.7476,5.7379
2023-04-23T16:26:56.241-07:00,1.8049,2.8965,3.9417,4.9424,5.9350
2023-04-23T16:26:57.342-07:00,2.0429,3.0110,4.0871,5.1015,6.0990
2023-04-23T16:26:58.445-07:00,2.2364,3.1074,4.2025,5.2334,6.2380
```

```python
import pandas as pd

data = pd.read_csv(
    "data_log.csv",
    header=7,
    parse_dates=["timestamp"],
)

print(f"shape{data.shape}")
axes = data.plot.line(x="timestamp")
```

> ```
> data.shape(108, 6)
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
- Add log file path control to main UI
- Detect software and hardware resources on host system
- Add dynamic DAQmx API detection and use
