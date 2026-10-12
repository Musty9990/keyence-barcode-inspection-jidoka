# I/O and tag summary

This is a partial tag summary extracted from the supplied project documentation and visible LAD printout. The complete I/O table is not present in the supplied overview report. Verify all mappings in the actual TIA Portal project and the separate I/O list before using this as a wiring reference.

| Address | Tag shown | Type / role | Notes |
|---|---|---|---|
| `E0.0` | `GetTheTrig` | Digital input | Operator trigger |
| `E0.1` | `Reset` | Digital input | Reset input |
| `E4.0` | `ReadComplete` | Digital input/status | Reader completion signal shown in the printout |
| `E5.0` | `ReadFail` | Digital input/status | Reader failure signal shown in the printout |
| `A0.0` | `Red` | Digital output | Red indication |
| `A0.2` | `yellow` | Digital output | Yellow indication |
| `A0.3` | `Greeen` | Digital output | Green indication; spelling follows export |
| `A4.0` | `clear` | Digital output/tag | Clear signal shown in the printout; confirm actual mapping |
| `A2.7` | `ErrorClear` | Digital output/tag | Brief error-clear pulse shown in the printout |
| `A3.0` | `TrigStatus` | Digital output/tag | Trigger status indication shown in the printout |

## Internal flags visible in the printout

| Tag | Address | Purpose described/inferred from tag and network labels |
|---|---|---|
| `ReadActive` | `M7.0` | Read-cycle active flag |
| `ReadFinish` | `M7.1` | Read-finish flag |
| `NOREAD` | `M7.5` | No-read state |
| `TIMEOUT` | `M7.6` | Timeout state |
| `LinkErrr` | `M10.0` | Device link error |
| `GenErr` | `M10.1` | General error flag |
| `RESComErr` | `M20.4` | Communication-error reset/handling flag |
| `Hard_Reset` | `M20.5` | Reset-related flag |
| `Ok` | `M4.4` | OK result flag |
| `NG` | `M4.1` | NG result flag |

> **Caution:** Address/tag names are reproduced from the provided printout, including apparent spelling inconsistencies. This table is not a complete electrical I/O list. Do not wire hardware based on this partial summary alone.
