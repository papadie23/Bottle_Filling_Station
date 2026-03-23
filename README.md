# Bottle Filling Station — TIA Portal & SCADA

A university automation project built around a simulated industrial bottling line. The system handles everything from mixing drink ingredients to labeling the final bottles — all controlled through a Siemens PLC and monitored via a custom SCADA interface.

---

## What is this?

This is a practical lab project from my 4th year at the Faculty of Automation and Computer Science, TUIAȘI. The goal was to program a complete sequential control system for a bottle filling station using **Siemens TIA Portal**, and then build a **SCADA interface** to visualize and control the process in real time.

The whole thing runs on a **Siemens S7-300/S7-1500 PLC** and uses the **GRAPH language** (Sequential Function Chart) to model the production flow step by step.

---

## How the process works

The production cycle goes through 8 steps, looping until 10 bottles are filled:

- **S1 – Home** resets the bottle counter and prepares for a new batch
- **S2 – Fill Recipe** opens the valves for water, apple juice concentrate, and orange juice concentrate — each for a duration set from the HMI
- **S3 – Mixer** runs the mixer for 4 seconds, then waits for it to stop before moving on
- **S4 – Transport Filling** starts the conveyor and waits 5 seconds for the bottle to reach the filling station
- **S5 – Filling** opens the filling valve for 3 seconds and increments the bottle counter
- **S6 – Transport Labeling** moves the bottle to the labeling station
- **S7 – Labeling** applies the best-before date label
- **S8 – Filling Complete** only runs after all 10 bottles are done, then restarts from S1

---

## SCADA Interface

The SCADA screen gives you a live view of the entire line — you can see which step is active, monitor the bottle count, set recipe durations for each ingredient, and handle any group faults without touching the PLC directly.

Built in WinCC as part of the TIA Portal project.

---

## Key tags

| Tag | Address | What it does |
|-----|---------|--------------|
| `GRAPH_Group_Fault` | M10.0 | Halts the sequencer on any error |
| `GRAPH_Count_Bottle` | MW12 | Tracks how many bottles have been filled |
| `GRAPH_Mixer_ON` | Q1.0 | Mixer output |
| `Valve_water` / `Valve_AJC` / `Valve_OJC` | Q1.1–Q1.3 | Ingredient valves |
| `Valve_Fill_Bottle` | Q1.4 | Filling valve |
| `Conveyor_Start_Conveyor` | M0.0 | Starts the belt for a timed run |

---

## Stack

- TIA Portal v16+
- GRAPH (SFC) for the main sequencer
- STL for the conveyor control block
- SCL for the best-before date calculation
- WinCC for the SCADA/HMI interface
- Target hardware: S7-1500 (or S7-300 Master)

---

## Running it

1. Open the project in TIA Portal
2. Compile everything: right-click the CPU → *Compile → Hardware and software*
3. Download to the PLC
4. Open the SCADA screen and hit Start

If you're running it without physical hardware, use PLCSIM to simulate the PLC locally.

---

Made by **Cosmin Vleju** — Automation & CS, TUIAȘI

[github.com/papadie23](https://github.com/papadie23) · cosmineugen23@gmail.com
