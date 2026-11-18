# Automated Conveyor Belt System

A simulated industrial conveyor control system developed using **CODESYS V3.5** and **Ladder Logic**. This project demonstrates PLC motor control, operating interlocks, VFD speed-reference simulation, jam detection, alarm reset, and package counting.

## Project Overview

The goal of this project was to build and test a small conveyor-control application in a PLC simulation environment. The logic was developed in CODESYS and tested using the runtime and watch/monitoring values.

**This is a software simulation.** It is not connected to a physical conveyor, VFD, motor, or safety circuit.

## Tools and Technologies

- CODESYS V3.5
- Ladder Diagram (LD)
- CODESYS Control Win runtime
- IEC 61131-3 PLC programming concepts

## Main Features

- **Start/stop control:** Latching conveyor run logic.
- **Operating interlocks:** Start permission depends on the simulated E-stop status, overload status, and VFD-ready status.
- **VFD speed simulation:** While the simulated drive is running, the actual-frequency value follows the configured speed reference; when stopped, the simulated frequency returns to zero.
- **Jam detection:** A TON timer detects a jam condition after the sensor input remains active for the configured delay. The jam alarm is latched and can be reset when the sensor is clear.
- **Package counting:** A CTU counter increments from package-sensor input pulses and can be reset.

## How the Logic Works

1. The start/stop network controls the conveyor run command and uses a holding contact to maintain the run state.
2. The interlocks prevent or stop operation when a required permissive is not present.
3. The VFD simulation uses the drive-running status and speed reference to calculate the simulated actual frequency.
4. The jam timer monitors the jam-sensor input. When the timer reaches its preset time, the jam condition sets the latched alarm.
5. The package counter counts package-sensor pulses and resets when the reset input is activated.

## Testing Performed

The following behaviours were tested in the CODESYS simulation:

- Conveyor start/stop operation and operating interlocks.
- VFD speed-reference tracking at **20 Hz, 30 Hz, and 40 Hz** while the simulated drive was running.
- Jam detection after the configured timer delay.
- Jam-alarm reset after the jam sensor was cleared.
- Package-counter reset and counting; the counter was observed reaching five.

These are simulation test results, not tests of physical equipment.

## Repository Contents

- `CODESYS_Project/` — CODESYS project file.
- `Documentation/` — project documentation.
- `Screenshots/` — screenshots and test evidence.

## Engineering Notes and Limitations

- The E-stop and overload signals in this project are simulated logic inputs. They do **not** represent a safety-rated emergency-stop or overload-protection system.
- The VFD and motor behaviour are simulated in PLC logic; no physical drive or motor is controlled.
- The project is intended as a learning and portfolio demonstration. A real machine would require a proper risk assessment, validated safety hardware and circuits, and commissioning by qualified personnel.
- The project contains both prefixed and non-prefixed speed-reference/frequency variable names. The active VFD simulation network uses `VFD_Speed_Reference` and `VFD_Actual_Frequency`; refer to the project documentation when reviewing the variable list.

## Possible Future Improvements

- Add an HMI screen for operator commands, status, and alarms.
- Expand fault handling and alarm diagnostics.
- Add additional sensor and conveyor-zone simulations.
- Test and document more operating and fault scenarios.
- Connect to suitable physical hardware only after appropriate engineering and safety design.

## Learning Outcomes

This project provided practical experience with Ladder Logic, PLC latching circuits, permissive interlocks, timer and counter function blocks, watch-table testing, and documenting PLC simulation results.
