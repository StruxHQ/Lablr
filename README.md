# Lablr

**A standalone Wi-Fi label printer built from a DYMO LabelWriter and an ESP32-S3.**

Lablr connects a DYMO LabelWriter directly to an ESP32-S3 over USB. It stores SVG labels, renders them on-device with ThorVG, and prints them over Wi-Fi — no PC, Raspberry Pi, or server required.

Use the built-in web interface or send commands over a local WebSocket. For remote access, the optional [Strux Relay](https://github.com/vanBassum/strux-relay) also lets MCP clients such as ChatGPT discover and control the printer. Lablr is built on [Strux](https://github.com/vanBassum/Strux), which provides Wi-Fi setup, the web UI, OTA updates, settings, and command routing.

<img width="1096" height="591" alt="Lablr web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## Hardware

- ESP32-S3 with **16 MB flash and 8 MB octal PSRAM** (currently supported board)
- DYMO LabelWriter connected to the ESP32-S3 native USB host
- External **5 V VBUS supply** for the USB printer connection
- Wi-Fi network

The current print implementation targets a 300-DPI, 672-dot LabelWriter print path. Other models are not automatically supported.

## Getting started

1. Download `Lablr-factory.bin` from the [latest release](https://github.com/vanBassum/Lablr/releases).
2. Open [ESP Web Flasher](https://espressif.github.io/esptool-js/) in Chrome or Edge, select the ESP32-S3 serial port, and flash the factory binary at offset `0x0`.
3. On first setup, connect to the `Lablr-AP` access point and use the device's web interface to configure Wi-Fi.
4. Open the device's web interface on your network to manage labels and printing.

For development from source, install [ESP-IDF v6.0+](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/), [Node.js 22+](https://nodejs.org/), and [pnpm](https://pnpm.io/).

## Extending Lablr

The printer-specific implementation lives in `main/app/`, including `UsbHostManager`, `PrintManager`, and `RenderManager`. Supporting another printer means implementing its USB/print protocol and adapting the print path; it is not just a configuration change.

Board-specific definitions live under `main/hardware/boards/`. Adding a different ESP32 board requires its own board configuration and suitable USB-host hardware, flash, and PSRAM.

The reusable application foundation lives in `main/strux/`. See [Strux](https://github.com/vanBassum/Strux) for the framework and its architecture.

## Tech stack

| Layer | Technology |
| --- | --- |
| Firmware | C++, ESP-IDF v6.0 |
| Web UI | React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| Hardware | ESP32-S3, 16 MB flash, 8 MB octal PSRAM |
| Printing | DYMO LabelWriter over USB host, ThorVG SVG rendering |
| CI/CD | GitHub Actions for tests, builds, and releases |

## License

No license is currently specified. All rights are reserved unless a license is added.
