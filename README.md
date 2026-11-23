# CarnLog Hardware

An OBD II datalogger that plugs into a vehicle's diagnostic port and records CAN bus, engine, and vehicle data over LTE and BLE.

## What It Does

Modern cars expose a wealth of data through the OBD II port: engine RPM, vehicle speed, coolant temperature, fuel status, diagnostic trouble codes, and raw CAN bus frames. Most of this data is only visible while you're sitting in the driver's seat with a scanner plugged in.

CarnLog removes that limitation. Once connected to the OBD II port, it continuously captures vehicle data and transmits it off-board — either over LTE for remote fleets or over BLE for local access — so the data can be logged, analyzed, and acted on without anyone present.

## Hardware Architecture

The design is built around three core subsystems:

### Cellular Modem — Quectel EC200U
Provides LTE connectivity for transmitting logged data to a remote server. The modem handles its own power management and network registration independently of the main controller.

### Main Controller — Nordic nRF52840
A low-power ARM Cortex-M4 with integrated BLE. Runs the application firmware, manages the CAN interface, buffers logged data, and handles communication with both the LTE modem and any local BLE client.

### Vehicle Interface — CAN Controller
Connects to the vehicle's CAN bus through the OBD II connector. Captures standard OBD II PIDs as well as raw CAN frames for deeper diagnostics.

### Power
Draws power directly from the vehicle's OBD II pin 16 (12V battery) with regulation down to the 3.3V rails needed by the logic. The nRF52840's low-power modes allow the logger to sleep between capture windows and wake on CAN activity.

## Data Flow

```
OBD II Port → CAN Bus → nRF52840 → Buffer → EC200U (LTE) / BLE
```

1. CAN frames arrive from the vehicle bus
2. The nRF52840 parses and timestamps them
3. Data is buffered in flash during transit gaps
4. Buffered data is pushed over LTE or read locally over BLE

## Repository Contents

| File | Description |
|------|-------------|
| `CarnLog-26.PcbDoc` | PCB layout |
| `CarnLog-26.PrjPcb` | Altium project file |
| `CarnLog-26.pdf` | Schematic and assembly drawings |
| `overview.SchDoc` | Top-level system schematic |
| `pwr.SchDoc` | Power regulation and distribution |
| `can&usb.SchDoc` | CAN transceiver and USB interface |
| `ec200u.SchDoc` | LTE modem interface |
| `nrf52840.SchDoc` | BLE controller and peripherals |

## Use Cases

- **Fleet tracking** — monitor engine health and driving behavior across vehicles remotely
- **Diagnostic logging** — capture intermittent fault codes that only appear while driving
- **Development** — access raw CAN data from a vehicle for prototyping and testing
- **Insurance / telematics** — record driving patterns for usage-based insurance programs
