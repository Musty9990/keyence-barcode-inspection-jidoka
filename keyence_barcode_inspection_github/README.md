# Barcode Inspection and Jidoka Demonstration

A desktop-scale industrial automation project demonstrating barcode-based quality decisions using a Siemens SIMATIC S7-1200 PLC and a Keyence SR-X100W barcode reader.

> **Project status:** Educational / desktop demonstration. The HMI is simulated in WinCC on a PC. This repository documents the demonstrated scope; it is not a production-ready machine-control package.

## Overview

The PLC triggers a barcode-reading cycle, receives the read status and barcode data, and classifies a successfully read barcode against a reference list. The first five successfully read barcode strings are used as reference entries. A match produces an **OK** result; a readable barcode that does not match produces **NG**. The program also handles no-read/timeout and camera communication-error conditions, with visual status indication.

The project demonstrates a simple **Jidoka-style** response: the inspection result is made visible so that an operator can distinguish acceptable, non-matching, and error conditions.

## System components

| Component | Role |
|---|---|
| Siemens SIMATIC S7-1200 CPU 1215C DC/DC/DC | Trigger/read sequence, barcode comparison, status handling, error handling and reset |
| Keyence SR-X100W barcode reader | Reads barcodes and returns status/data to the PLC |
| WinCC simulation on a PC | Software HMI/operator display; no physical HMI panel was used |
| Patlite K50LGRAL1YPQ | Visual/audible indication: yellow at trigger, brief buzzer on read event, green for OK, red for NG |
| TIA Portal LAD program | PLC logic and device-data configuration |

Exact wiring, complete addressing and device configuration should be taken from the supplied project printout and I/O documentation, not inferred from this overview.

## Process sequence

1. The operator activates the trigger input (`E0.0`, tag `GetTheTrig`).
2. The PLC starts a read cycle and indicates the trigger event in yellow.
3. The Keyence reader returns read status and barcode data. A short buzzer indication is associated with a read event.
4. The PLC converts the received character data into a string and compares it with the reference entries.
5. A match sets the OK status and green indication. A readable non-match sets NG and the red indication.
6. If the read does not complete within the configured **8-second timeout**, the program indicates `TIMEOUT`. A failed read is handled as `NOREAD`; a reader communication/link fault is handled as a communication error (`COMERR`/related link-status flags).
7. The operator activates the reset input (`E0.1`, tag `Reset`) to clear relevant statuses and counters for another demonstration run.

See [`docs/sequence.md`](docs/sequence.md) for the sequence and status definitions.

## PLC logic documented in the printout

The supplied TIA Portal printout shows the following networks:

- `LinkErr` — reader/device link status
- `ComErr` — communication-error reset handling
- `Trig` — trigger edge, read activation and associated state handling
- `timeout` — 8-second TON timeout
- `readcompleted` — read-completion edge handling
- `Noread` — failed-read handling and error/result text
- `Ok` — barcode-to-string handling, reference comparisons and OK indication
- `NG` — non-matching barcode handling and NG indication
- `ReadComplete` — completion indication and output cleanup
- `cleanUp` — read-active and error-state cleanup
- `ComErrBackUp` — communication-error recovery indication
- `Reset` — reset of statuses and counters

The exported printout identifies the main block as `Main_1 [OB123]`, language LAD, version 0.1. Confirm block organization and addressing in the actual TIA Portal project before reusing the program.

## Selected signals visible in the provided printout

This is a **partial summary**, not a substitute for the complete I/O list.

| Address / tag shown | Meaning in the printout |
|---|---|
| `E0.0` / `GetTheTrig` | Operator trigger |
| `E0.1` / `Reset` | Reset |
| `E4.0` / `ReadComplete` | Reader read-complete status |
| `E5.0` / `ReadFail` | Reader read-fail status |
| `A0.0` / `Red` | Red indication |
| `A0.2` / `yellow` | Yellow indication |
| `A0.3` / `Greeen` | Green indication |
| `A4.0` / `clear` | Clear signal shown in the printout |
| `M7.5` / `NOREAD` | No-read status flag |
| `M7.6` / `TIMEOUT` | Timeout status flag |
| `M10.0` / `LinkErrr` | Link-error flag |
| `M4.1` / `NG` | NG status flag |
| `M4.4` / `Ok` | OK status flag |

Names and spelling above follow the exported printout where possible. Validate physical I/O mapping against the actual hardware configuration before commissioning.

## Reference files

- [`docs/reference/keyence_barcode_inspection_project_report.pdf`](docs/reference/keyence_barcode_inspection_project_report.pdf) — project overview, component roles, process and scope.
- [`docs/reference/Keyence_Camera_Project_Trees_View.pdf`](docs/reference/Keyence_Camera_Project_Trees_View.pdf) — exported TIA Portal LAD/network printout.

The overview report says the final test was carried out on **9 October** and recorded on video. No video file is included in this repository package.

## Validation checklist

The project documentation identifies the following scenarios as relevant for validation. Record actual observed results before marking a test as passed.

- [ ] Known barcode matching one of the five reference entries → OK / green
- [ ] Successfully read barcode not in the reference list → NG / red
- [ ] Reader reports read failure → NOREAD handling
- [ ] No completion within 8 seconds → TIMEOUT handling
- [ ] Reader communication/link loss → communication-error handling
- [ ] Communication restored → recovery behavior
- [ ] Reset input clears the intended statuses and counters
- [ ] Repeated cycles do not leave stale result indications



## Known scope and limitations

- This is a desktop demonstration of an inspection concept, not a complete production-line installation.
- The operator interface is a WinCC PC simulation; no physical HMI panel was used.
- The first five successfully read barcode strings form the reference list in the described demonstration.
- The project report describes external valid-barcode storage, SQL Server logging and richer WinCC result/alarm display as possible future work, not as completed features.
- The repository does not include a native TIA Portal archive (`.zap`), full source project, video, complete wiring drawings or full I/O list unless separately added by the project owner.
- Safety-rated functions and production risk assessment are outside the documented scope.

## Possible next steps

1. Add a clear, versioned project export and a tested restore/import procedure.
2. Complete and verify the I/O map and hardware/network diagram.
3. Add a WinCC screen for latest barcode, OK/NG result, timeout and communication alarms.
4. Implement and document an externally managed valid-barcode table if required.
5. Add SQL Server logging only after the required schema, connectivity and error-handling behavior are defined.
6. Execute and record the test cases in `docs/test-plan.md`.
7. Add a short demonstration video or GIF, after checking that it contains no confidential information.

## Reproduction and software requirements

This repository is documentation-first. The supplied PDF printout is not sufficient to rebuild or download the PLC program by itself.

To open or modify the actual automation project, use a compatible Siemens TIA Portal installation and the original project/archive, plus the required Keyence device configuration and applicable hardware support. Exact software versions and device package versions are not specified in the supplied documents; verify compatibility from the original project.

## Safety and confidentiality

This repository is intended for educational demonstration and portfolio review. Do not deploy the logic to production equipment without engineering review, complete validation, suitable risk assessment and verification of the machine's safety functions. Do not publish customer/plant network details, credentials, production data or confidential project files.

## Author



Mustafa Yurtseven
- LinkedIn: https://www.linkedin.com/in/mustafa-yurtseven-769922284/
