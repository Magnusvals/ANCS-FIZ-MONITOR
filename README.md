# ANCS – ESP32 FIZ Monitor

3D Case Files for mounting on a Video Assist: [Thingiverse](https://www.thingiverse.com/thing:7295004)

### Camera Focus / Iris / Zoom Wireless Monitor

Firmware for the **ANCS FIZ Monitor Node**, an ESP32-based wireless camera control monitor designed for distributed film / broadcast environments.

This device receives real-time Focus and Zoom data over **ESP-NOW** and visualizes it on:

* OLED display
* Tally LED

It can automatically switch between:

* **Remote Mode (ESP-NOW Client)**
* **Standalone Configuration Mode (Access Point + Web GUI)**

---

## ✨ Features

* 📡 ESP-NOW wireless communication
* 🎯 Real-time Focus + Zoom monitoring
* 🔴🟢🔵 Tally LED indication (PGM / PVW / Status)
* 🖥 OLED FIZ display
* 🌐 Built-in captive portal WebGUI
* 💾 Persistent configuration storage (NVS)
* 🛠 MAC-address pairing system
* 🔄 Automatic fallback to AP mode
* 🧹 Factory reset via serial terminal

---

## 📦 Hardware Requirements

| Component    | Description                   |
| ------------ | ----------------------------- |
| ESP32        | Any ESP32-S3 compatible board |
| SSD1306 OLED | 72x40 I²C display             |
| WS2812 LED   | Single NeoPixel tally LED     |

### Pin Configuration

| Function | GPIO |
| -------- | ---- |
| OLED SDA | 41   |
| OLED SCL | 40   |
| LED Data | 39   |

---

## 📡 Wireless Operation

The FIZ Monitor communicates using **ESP-NOW** on a configurable Wi-Fi channel.

Incoming packets must contain:

* Sender MAC
* Target Base MAC
* FIZ Data Struct



## 🔌 Boot Modes

### Remote Mode (Default)

On boot the device will:

1. Start in ESP-NOW Station Mode
2. Wait for Base communication
3. Display incoming FIZ data

---

### Standalone Mode (Fallback)

If no valid signal is received within:

```
15 seconds
```

The device will automatically start a configuration Access Point.

SSID format:

```
ANCS-FIZ-XXXXXXXXXXXX
```

Password:

```
12345678
```

---

## 🌐 Web Configuration Portal

Connect to the device AP and open:

```
http://192.168.4.1
```

From here you can configure:

* Base MAC address
* Remote MAC address
* ESP-NOW Wi-Fi channel

Settings are stored in non-volatile memory.

---

## 🧹 Factory Reset

Within **3 seconds after boot**:

Send:

```
CR or LF
```

from the serial terminal to erase:

* Base MAC
* Remote MAC
* Wi-Fi Channel

Device will reboot automatically.

---

## 🔴 Tally LED Status

| State     | Color   |
| --------- | ------- |
| Off       | LED Off |
| PGM       | Red     |
| PVW       | Green   |
| PGM + PVW | Red     |
| AP Mode   | Blue    |

---

## 🛠 Libraries Used

* FastLED
* U8g2
* Preferences
* WiFi
* ESP-NOW
* WebServer
* DNSServer

Install using Arduino Library Manager.

---

## 📄 License

This project is licensed under the **GNU GPL v3** License.

Copyright (C) 2026
Magnus Valsgård

---

## 🔗 Project

Part of the ANCS wireless camera control ecosystem.
