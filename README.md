# Lablr

**Turn a USB DYMO LabelWriter into a standalone Wi-Fi label printer with an ESP32-S3.**

Lablr stores labels as SVG files, previews them in a browser, and prints them directly from the ESP32-S3. The device renders the SVG with ThorVG and sends it to the printer over USB. No PC, Raspberry Pi, or server is needed.

Control it through the built-in web interface or a local WebSocket. Optionally, [Strux Relay](https://github.com/StruxHQ/strux-relay) enables remote control, including through ChatGPT using MCP.

<img width="1096" height="591" alt="Lablr web interface" src="https://github.com/user-attachments/assets/cc282e06-f84b-497d-8e5a-3e04add95bac" />

## Hardware

- ESP32-S3 with **16 MB flash and 8 MB octal PSRAM**
- DYMO LabelWriter connected to the ESP32-S3's USB host
- External **5 V VBUS supply** for the printer's USB connection
- Wi-Fi

The current implementation targets a **300-DPI, 672-dot** LabelWriter print path. Other printer models may require changes.

## Getting started

1. Download `Lablr-factory.bin` from [Releases](https://github.com/StruxHQ/Lablr/releases).
2. Open [ESP Web Flasher](https://espressif.github.io/esptool-js/) in Chrome or Edge and flash the binary at offset `0x0`.
3. Connect to `Lablr-AP` to configure Wi-Fi.
4. Open the device's web interface to create, preview, and print labels.

## Development

The printer code lives in `main/app/`. Supporting another printer requires adapting the USB protocol and print pipeline; supporting another board requires its own hardware configuration.

Lablr is built on [Strux](https://github.com/StruxHQ/Strux), an ESP32 application template providing networking, web UI, OTA updates, and settings. See that repository for framework details and build prerequisites.

## License

No license is currently specified. All rights are reserved unless a license is added.
