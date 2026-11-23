# CarnLog Hardware

Design files for the CarnLog hardware: an LTE, BLE, and USB Full-Speed OBD II datalogger for modern vehicles.

## Overview

CarnLog is a vehicle datalogger that connects to a car's OBD II port and records diagnostic and CAN bus data. It combines:

- **Quectel EC200U** — LTE modem for cellular connectivity
- **Nordic nRF52840** — BLE and main controller
- **CAN controller** — vehicle bus interface

## Repository Contents

| File | Description |
|------|-------------|
| `CarnLog-26.PcbDoc` | PCB layout |
| `CarnLog-26.PrjPcb` | Altium project file |
| `CarnLog-26.pdf` | Schematic/assembly PDF |
| `overview.SchDoc` | Top-level schematic |
| `pwr.SchDoc` | Power supply schematic |
| `can&usb.SchDoc` | CAN and USB interface schematic |
| `ec200u.SchDoc` | LTE modem schematic |
| `nrf52840.SchDoc` | BLE controller schematic |

## Contributors

- [xmoshte](https://github.com/xmoshte) — hardware design and layout
- [WuodOdhis](https://github.com/WuodOdhis) — documentation

## License

See repository for license details.
