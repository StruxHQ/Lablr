# Lablr

**Turn a USB DYMO LabelWriter into a standalone network label printer with an ESP32-S3.**

Lablr connects a DYMO LabelWriter to an ESP32-S3 over USB host. Create labels as SVG files, preview them, and print them over Wi-Fi. The ESP32 renders the SVG with ThorVG and sends the raster data to the printer. No Raspberry Pi, cloud account, or always-on server is required for local use.

You can control Lablr from its browser-based interface or send commands over a local WebSocket connection. If you *want* remote access, the optional [Strux Relay](https://github.com/vanBassum/strux-relay) connects the device to external clients, including AI assistants through MCP. The device advertises its available commands, so clients can discover how to operate it.

Lablr is a real-world application built on [Strux](https://github.com/vanBassum/Strux), an ESP32 application template that provides Wi-Fi setup, a React web UI, OTA updates, settings, and command routing. The printer-specific code lives in `main/app/`; the reusable framework lives in `main/strux/`.

> **Photo coming soon:** A picture of the ESP32-S3, connected LabelWriter, and printed label will go here. The screenshot below shows the current web interface.

<img width="1096" height="591" alt="Lablr web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## Hardware and setup

- ESP32-S3 with **16 MB flash and 8 MB octal PSRAM** (the currently supported board).
- A compatible DYMO LabelWriter connected to the ESP32-S3's native USB host pins.
- **External 5 V USB VBUS power** for the printer connection; the board cannot supply it directly.
- Wi-Fi for network access.

**Quick start:** Flash the latest [factory firmware release](https://github.com/vanBassum/Lablr/releases) using the browser-based method below, connect to the device's `Lablr-AP` fallback access point to configure Wi-Fi, and open its web interface. The sections below cover building from source, board configuration, and the printing internals.

**Note:** The current implementation targets the documented 300-DPI, 672-dot LabelWriter print path; do not assume every DYMO model is supported.

## Tech Stack

Build on on Strux

| Layer | Stack |
|-------|-------|
| Firmware | C++, ESP-IDF v6.0 |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| Target | ESP32-S3 (16 MB flash, 8 MB octal PSRAM) |
| Printer | DYMO LabelWriter over USB host, 300 DPI, 672-dot head |
| CI/CD | GitHub Actions — host tests, frontend and firmware on every push; releases on a `v*` tag |

## Getting Started

### Prerequisites

- [ESP-IDF v6.0+](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/)
- [Node.js 22+](https://nodejs.org/) and [pnpm](https://pnpm.io/)


INSERT HERE: 
How to port to another device, how to support another printer


## License

This project is unlicensed. Use it however you want.
