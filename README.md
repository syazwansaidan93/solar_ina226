# ESP32 Solar Battery Monitor & Relay Controller

A lightweight ESP32-based solar battery monitoring and relay control system with a built-in web dashboard, INA226 power monitoring, automatic battery protection, OTA firmware updates, and JSON API support.

## Features

* Real-time battery voltage monitoring
* Current and power measurement using INA226
* Automatic relay control based on battery voltage and charging current
* Battery percentage estimation
* Energy consumption tracking (Wh)
* Peak voltage, current, and power logging
* Web-based dashboard (mobile friendly)
* REST JSON API
* OTA firmware update via browser
* Persistent configuration storage using Preferences
* Event logging system
* NTP time synchronization
* Automatic daily statistics reset
* Wi-Fi auto reconnect

---

## Hardware Requirements

### Supported Hardware

* ESP32
* INA226 Current/Voltage Sensor
* Relay Module
* 12V Lead Acid / AGM Battery
* Solar Charge Controller (optional)
* Wi-Fi Network

### GPIO Configuration

| Function     | GPIO   |
| ------------ | ------ |
| Relay Output | GPIO 5 |
| INA226 SDA   | GPIO 8 |
| INA226 SCL   | GPIO 9 |

---

## Configuration

Default network settings:

```cpp
IPAddress local_IP(192,168,1,6);
IPAddress gateway(192,168,1,1);
IPAddress subnet(255,255,255,0);
```

Wi-Fi SSID:

```cpp
const char* ssid = "wifi_slow2";
```

NTP Server:

```cpp
const char* ntpServer = "192.168.1.1";
```

---

## Battery Protection Logic

### Relay ON

Relay will activate when:

```text
Battery Voltage <= Low Cutoff Voltage
```

### Relay OFF

Relay will deactivate when:

```text
Battery Voltage >= High Threshold Voltage
AND
Charging Current >= Current Threshold
```

### Debounce Protection

State changes must remain stable for:

```text
60 seconds
```

before the relay is switched.

---

## Web Dashboard

The built-in web interface provides:

* Battery percentage
* Voltage
* Current
* Power
* Energy usage (Wh)
* Peak statistics
* Relay status
* Relay runtime
* Event logs
* Configuration page
* OTA update page

Accessible through:

```text
http://ESP32_IP/
```

---

## REST API

### Endpoint

```text
GET /api/data
```

### Example Response

```json
{
  "voltage": 13.45,
  "current_ma": 850.0,
  "power_mw": 11400.0,
  "battery_pct": 92.5,
  "relay": 0,
  "energy_wh": 125.8,
  "timestamp": "2026-06-17 12:34:56"
}
```

---

## OTA Firmware Update

Firmware can be updated directly from the web interface.

1. Open:

```text
http://ESP32_IP/update
```

2. Upload the compiled `.bin` file.
3. Device automatically reboots after successful update.

---

## Data Persistence

The following settings are stored in ESP32 flash memory:

* Low voltage cutoff
* High voltage threshold
* Current threshold
* Voltage calibration offset
* Last relay state

Storage backend:

```cpp
Preferences
```

---

## Daily Maintenance Tasks

### 06:30 AM

Automatically resets:

* Peak Voltage
* Peak Current
* Peak Power
* Energy Counter (Wh)

### 12:00 PM

Automatically resets:

* Relay Runtime Counter

---

## Event Logging

The system stores recent events such as:

* Wi-Fi connected/disconnected
* NTP synchronization
* Relay ON/OFF events
* Configuration changes
* Daily resets
* Manual relay operations

---

## Build Environment

Recommended:

* Arduino IDE
* ESP32 Arduino Core
* INA226 Library

Required libraries:

```text
WiFi
WebServer
Preferences
Wire
INA226
Update
time
```

---

## License

MIT License

Feel free to modify, improve, and use this project for personal or commercial applications.

---

## Screenshots

Add screenshots of:

* Dashboard
* Configuration page
* OTA update page
* API output

to showcase the project features.
