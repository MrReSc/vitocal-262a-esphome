# Viessmann Vitocal 262-A - ESPHome CAN Integration

Direct CAN bus integration of the Viessmann Vitocal 262-A heat pump into Home Assistant
using ESPHome on an ESP32-S3. No cloud, no Viessmann ViCare app required.

**Compatibility:** This integration is developed and tested exclusively with the
**Vitocal 262-A with OneBase / E3 control unit**. It will likely not work with other
Vitocal models or older control units.

---

## Disclaimer

This project is provided as-is, without any warranty or guarantee of any kind.
Use at your own risk. I accept no responsibility for any damage to your heat pump,
heating system, or any other equipment.

Parts of this project were developed with the assistance of Claude Sonnet 4.6.

---

## What this is

The ESP32-S3 connects to the heat pump's internal CAN bus and speaks the
UDS (ISO 14229 / ISO 15765-2) diagnostic protocol. It reads sensor values and writes
control parameters (e.g. hot water setpoint) directly to the heat pump, without any
internet connection. All data stays local and integrates natively with Home Assistant
via the ESPHome API.

---

## Hardware

- **ESP32-S3** (any board with exposed GPIO pins)
- **SN65HVD230** CAN transceiver

---

## Sensors & Controls

All entities exposed to Home Assistant:

| Entity | DID | Type | Unit |
|--------|-----|------|------|
| DomesticHotWaterSensor Actual | 0271 | sensor | °C |
| DomesticHotWaterBufferBottomTemperatureSensor | 3232 | sensor | °C |
| DomesticHotWaterBufferMidTemperatureSensor | 3233 | sensor | °C |
| DomesticHotWaterBufferTopTemperatureSensor | 3234 | sensor | °C |
| CurrentElectricalPowerConsumptionSystem | 2488 | sensor | W |
| CurrentThermalCapacitySystem | 2496 | sensor | W |
| EnergyConsumptionDomesticHotWater Today | 0565 | sensor | kWh |
| GeneratedDomesticHotWaterOutput Today | 1391 | sensor | kWh |
| COP Today | - | sensor (derived) | - |
| HeatPumpCompressorStatistical starts | 2369 | sensor | - |
| HeatPumpCompressorStatistical hours | 2369 | sensor | h |
| AdditionalElectricHeaterStatistical starts | 2370 | sensor | - |
| AdditionalElectricHeaterStatistical hours | 2370 | sensor | h |
| HeatPumpCompressor PowerState | 2351 | binary\_sensor | - |
| AdditionalElectricHeater PowerState | 2352 | binary\_sensor | - |
| DomesticHotWaterStatus | 2320 | text\_sensor | Idle/Active/Postrun |
| Date | 0505 | text\_sensor (diagnostic) | - |
| Time | 0506 | text\_sensor (diagnostic) | - |
| SoftwareVersion | 0580 | text\_sensor (diagnostic) | - |
| HardwareVersion | 0581 | text\_sensor (diagnostic) | - |
| DomesticHotWaterTemperatureSetpoint | 0396 | **number** (writable) | °C (35-60) |

---

## DID Reference

The heat pump exposes 360 Data Identifiers (DIDs) on its CAN bus. All of them are
documented with names and scan-time hex values in:

[docs/did_reference.md](docs/did_reference.md)

The raw scan files are in [scan/](scan/).

---

## open3e

The scan files in [scan/](scan/) were produced using [open3e](https://github.com/open3e/open3e).
For codec documentation, DID type definitions, and the full upstream Vitocal datapoint list, see:

[docs/open3e_links.md](docs/open3e_links.md)

---

## Credits

- [open3e](https://github.com/open3e/open3e) - CAN/UDS protocol library for Viessmann heat pumps
- [esphome-vitoair](https://github.com/maromme/esphome-vitoair) - ESPHome inspiration for Viessmann CAN integration
- [ESPhome-CAN-Viessmann](https://github.com/Parateam/ESPhome-CAN-Viessmann) - ESPHome CAN integration for Viessmann
