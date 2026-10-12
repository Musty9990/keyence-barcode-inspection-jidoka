# Test plan

Use this checklist during simulation or controlled bench testing. Fill in the observed result, date, software/hardware versions and evidence. Do not mark a test as passed until it has actually been run.

## Test record

- Test date:
- Tester:
- TIA Portal version:
- PLC firmware / CPU:
- Keyence SR-X100W configuration:
- Test environment: (simulation / desktop hardware / other)
- Project revision:

## Functional tests

| ID | Scenario | Expected behavior from project description | Observed result | Pass/Fail |
|---|---|---|---|---|
| TC-01 | Trigger a read cycle | Cycle starts; yellow trigger indication appears | | |
| TC-02 | Read a barcode matching a stored reference | OK status; green indication | | |
| TC-03 | Read a barcode that is not in the reference list | NG status; red indication | | |
| TC-04 | Reader reports a failed/no-read result | NOREAD handling and corresponding result/status | | |
| TC-05 | Reader does not complete within 8 seconds | TIMEOUT status is set/indicated | | |
| TC-06 | Reader communication/link is interrupted | Communication/link error is detected/handled | | |
| TC-07 | Restore reader communication | Recovery logic clears/recovers the relevant condition as designed | | |
| TC-08 | Activate reset input E0.1 | Intended status flags and counters are reset | | |
| TC-09 | Run consecutive reads | Old status/output indications do not incorrectly persist | | |
| TC-10 | Check read string conversion | Returned barcode string is compared correctly, including expected length/content | | |

## Evidence to attach

- Screenshot or video of the test
- Relevant TIA Portal online monitoring screenshot
- Reader result/status observed during test
- Any fault code and recovery steps
- Notes on discrepancies and corrective action

## Acceptance notes

The expected behavior above is based on the supplied project description. Where the exact expected output duration, counter behavior or recovery sequence is not specified, define the acceptance criterion before testing and document the decision. This is a portfolio/educational test plan, not a production qualification protocol.
