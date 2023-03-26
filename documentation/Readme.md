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
  - on-demand while running
- Logging
  - CSV format
  - create or overwrite log file
  - append to to existing log file

## Baseline

LabVIEW sample project: Continuous Measurement and Logging

- Launch LabVIEW and select Create Project. From the Create Project dialog, launch the Continuous Measurement and Logging sample project.
- NI site: https://www.ni.com/en-us/support/documentation/supplemental/21/using-a-queued-message-handler-in-labview.html
- LV wiki: https://labviewwiki.org/wiki/Design_pattern

## Changes

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
