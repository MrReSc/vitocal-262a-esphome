# open3e Reference

[open3e](https://github.com/open3e/open3e) is the Python library used to scan and
communicate with Viessmann heat pumps over CAN bus using the UDS (ISO 14229) protocol.

The files in [../scan/](../scan/) were produced by running open3e against the heat pump's
CAN address `0x680` (module HPMUMASTER). They are specific to this Vitocal 262-A unit
and are not part of the open3e project itself.

---

## Key Files in the open3e Repository

These are the files most relevant for understanding and extending the DID integration:

| File | Purpose |
|------|---------|
| [`src/open3e/Open3EdatapointsVcal.py`](https://github.com/open3e/open3e/blob/main/src/open3e/Open3EdatapointsVcal.py) | Vitocal-specific DID definitions (closest upstream reference for this device) |
| [`src/open3e/Open3Ecodecs.py`](https://github.com/open3e/open3e/blob/main/src/open3e/Open3Ecodecs.py) | Codec classes for decoding raw DID bytes (temperatures, enums, time schedules, etc.) |
| [`src/open3e/Open3Edatapoints.md`](https://github.com/open3e/open3e/blob/main/src/open3e/Open3Edatapoints.md) | Full DID reference with data types, units, and scaling factors |
| [`src/open3e/Open3Eenums.py`](https://github.com/open3e/open3e/blob/main/src/open3e/Open3Eenums.py) | Enum definitions for status and mode DIDs |
| [`src/open3e/Open3Edatapoints.json`](https://github.com/open3e/open3e/blob/main/src/open3e/Open3Edatapoints.json) | Machine-readable DID catalog (all supported devices) |

---

## Relationship to the Scan Files

`scan/Open3Edatapoints_680.py` is the output of scanning this specific heat pump.
It lists only the DIDs that responded on address `0x680`. Comparing it against
`Open3EdatapointsVcal.py` shows which upstream-defined DIDs are actually present
on this unit and which are absent.

`scan/virtdata_680.txt` contains the raw byte payloads returned for each DID during
the scan. These are input to `Open3Ecodecs.py` for decoding into human-readable values.
The decoded results for the active DIDs are documented in [did_reference.md](did_reference.md).

---

## open3e README

The open3e project README covers installation, usage, MQTT integration, and how to run
a device scan:

https://github.com/open3e/open3e/blob/main/README.md
