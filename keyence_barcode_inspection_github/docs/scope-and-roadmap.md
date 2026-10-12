# Scope and roadmap

## Documented current scope

- Siemens S7-1200 CPU 1215C DC/DC/DC running LAD logic.
- Keyence SR-X100W barcode reader.
- Trigger/read-completion/read-failure sequence.
- First five successfully read barcode strings used as reference entries.
- OK/NG comparison and indication.
- 8-second timeout handling.
- No-read and communication/link-error handling.
- Reset of relevant status and counters.
- WinCC PC simulation; no physical HMI panel.

## Items described as possible future work

These are not claimed as completed features:

- External valid-barcode table.
- SQL Server logging.
- Displaying barcode results and alarms in WinCC.
- Expanded recorded tests for successful reads, mismatches, no-read timeout, communication loss and recovery.

## Suggested implementation order

1. Confirm the baseline behavior and preserve a versioned backup of the working TIA Portal project.
2. Verify the complete I/O list, hardware configuration and network/device settings.
3. Define the data model for reference barcodes and decide whether the list remains PLC-resident or becomes externally managed.
4. Specify the HMI screen requirements and alarm/reset behavior.
5. If SQL logging is required, define schema, timestamp source, retry behavior, duplicate handling and behavior during database/network outage.
6. Execute and record the test plan.
7. Review all screenshots, diagrams and exports for confidential information before publishing.

## Out of scope

The supplied documents do not establish a production deployment, a safety-rated design, a complete electrical drawing package, a fully implemented SQL Server integration, or a completed external barcode database.
