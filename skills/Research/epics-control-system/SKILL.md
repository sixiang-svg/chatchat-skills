---
id: epics-control-system
name: EPICS Control System
description: Guidance on EPICS for accelerator and beamline control, including IOC configuration, channel access, and archiving.
category: Research
requires: []
examples:
  - Configure an Input/Output Controller (IOC) for a new beamline instrument.
  - Use caproto to script Channel Access monitoring for process variables.
---

# EPICS Control System

## Purpose

Provides expert guidance on EPICS for accelerator and beamline control systems, including IOC configuration and channel access.

## Instruction
- Configure Input/Output Controllers (IOCs) by defining the necessary database (.db) records and process variables (PVs).
- Define Channel Access (CA) protocols to monitor and control beamline instruments and experimental hardware.
- Integrate the Archiver Appliance or specialized archivers to log time-series data for long-term experiment monitoring.
- Design alarm handling logic to detect and respond to equipment status changes or safety threshold breaches.
- Develop Operator Interface (OPI) screens using Phoebus or specialized display managers for real-time visualization.
- Implement Python scripting via caproto or pyepics for automated instrument control and data acquisition.

## When to Use
- When deploying new IOCs or instruments for beamline and accelerator control environments.
- When automating hardware monitoring tasks or developing real-time control scripts.
- When configuring data archiving and alarm systems for mission-critical scientific facilities.

## Output
- IOC configuration files and PV database records for the target hardware.
- Functional control scripts for Channel Access monitoring and instrumentation logic.
- Alarm configuration summaries and archival setup plans for experiment tracking.

## Capabilities

- IOC configuration and deployment
- Channel Access protocol
- Archiver integration
- Alarm handling
- OPI screen development
- Python/caproto scripting

## Usage Guidelines

1. **IOC Setup**: Configure Input/Output Controllers
2. **Channels**: Define process variables and records
3. **Archiving**: Set up archiver for data logging
4. **Alarms**: Configure alarm handling
5. **Python Integration**: Use caproto or pyepics for scripting

## Tools/Libraries

- EPICS
- caproto
- pyepics
- phoebus
