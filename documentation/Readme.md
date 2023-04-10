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
  - create or overwrite log file
  - append to existing log file

## Data

```csv
Date,2023-03-26
Start time,11:17:41.972
timestamp,sim1,sim2,sim3,sim4
11:17:41.973,0.0000,1.0000,2.0000,3.0000
11:17:43.025,0.7887,1.7594,2.7467,3.7400
11:17:44.024,1.1867,2.1843,3.1664,4.1551
11:17:45.024,1.4064,2.4791,3.4673,4.4545
11:17:46.025,1.5567,2.6917,3.6980,4.6878
11:17:47.025,1.7251,2.8467,3.8800,4.8768
11:17:48.025,1.9351,2.9626,4.0255,5.0332
```

## Changelog

### Baseline

LabVIEW sample project: Continuous Measurement and Logging

- Launch LabVIEW and select Create Project. From the Create Project dialog, launch the Continuous Measurement and Logging sample project.
- NI site: https://www.ni.com/en-us/support/documentation/supplemental/21/using-a-queued-message-handler-in-labview.html
- LV wiki: https://labviewwiki.org/wiki/Design_pattern

### Changes

- Make the root container for Aquired Data.ctl a cluster
- Use typedefs in the data queues/notifiers rather than raw constants
- Add new-log/append-log tab control to Settings Dialog
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
