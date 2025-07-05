# Apollo Multi-target Motion Multisensor (MTR-1)

[![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-blue)](https://esphome.io/)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Ready-green)](https://www.home-assistant.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)

The Apollo MTR-1 is an advanced multi-sensor device that combines **motion detection**, **environmental monitoring**, and **presence sensing** in one compact package. Perfect for Home Assistant automation enthusiasts who want comprehensive room monitoring without multiple devices.

## ✨ Features

- **🎯 Multi-target Motion Detection** - Advanced LD2450 radar sensor for precise presence and movement tracking
- **🌡️ Environmental Monitoring** - Temperature, humidity, atmospheric pressure, and CO2 levels
- **☀️ Light & UV Sensing** - Ambient light and UV index measurement for smart lighting automation
- **🔊 Audio Feedback** - Built-in buzzer for notifications and alerts
- **💡 RGB Status Indicator** - Visual feedback with programmable LED strip
- **📶 Wireless Connectivity** - WiFi with optional Bluetooth Low Energy (BLE) proxy
- **🏠 Home Assistant Ready** - Native ESPHome integration with automatic discovery

## 📦 Quick Start

### Prerequisites
- [Home Assistant](https://www.home-assistant.io/) with [ESPHome Add-on](https://esphome.io/guides/getting_started_hassio.html) installed
- MTR-1 device (purchase from [Apollo Automation](https://apolloautomation.com))
- WiFi network credentials

### Initial Setup (New Device)
1. **Power on your MTR-1** - Connect via USB or 5V power supply
2. **Connect to device hotspot** - Look for "Apollo MTR1 Hotspot" in your WiFi networks
3. **Configure WiFi** - Follow the captive portal to connect device to your network
4. **Add to Home Assistant** - Device should auto-discover in Home Assistant notifications
5. **Install ESPHome configuration** - Use the dashboard import feature

### Manual ESPHome Configuration
If you prefer manual setup or customization:

1. **Copy configuration file** to your ESPHome dashboard
2. **Choose the right variant** for your needs (see Configuration Files section below)
3. **Compile and upload** firmware to your device
4. **Add to Home Assistant** via ESPHome integration

## 🔧 Configuration Files

This repository contains three ESPHome configuration variants:
### 📁 `MTR-1.yaml` - Standard Configuration
**Recommended for most users**
- Full sensor functionality with WiFi connectivity
- Web server interface for direct device access
- OTA (Over-The-Air) updates enabled
- Ideal for: General home automation, room monitoring

### 📁 `MTR-1_BLE.yaml` - Bluetooth Proxy
**For advanced Bluetooth integration**
- All standard features plus Bluetooth Low Energy proxy
- Extends Home Assistant's Bluetooth range
- Useful for Bluetooth device tracking and automation
- Ideal for: Smart locks, fitness trackers, BLE sensors

### 📁 `MTR-1_Factory.yaml` - Factory Firmware
**Pre-installed on new devices**
- Includes ESP32 Improv for easy WiFi setup
- Automatic transition to standard config after setup
- Factory testing and calibration features
- Ideal for: Initial device setup and onboarding

### 📁 `Core.yaml` - Shared Components
**Internal configuration file**
- Contains all sensor definitions and core functionality
- Shared across all variants to ensure consistency
- Includes calibration settings and hardware definitions
- Note: This file is automatically included by other configs

## 🚀 How to Use This Repository

### Method 1: Dashboard Import (Easiest)
1. **Open ESPHome Dashboard** in Home Assistant
2. **Click "+" to add new device**
3. **Select "Continue" for dashboard import**
4. **Enter this URL**: `github://ApolloAutomation/MTR-1/Integrations/ESPHome/MTR-1.yaml`
5. **Follow the setup wizard** to configure your device

### Method 2: Manual File Copy
1. **Download or clone** this repository
2. **Navigate** to `Integrations/ESPHome/` folder
3. **Copy your chosen YAML file** to your ESPHome config directory
4. **Copy `Core.yaml`** to the same directory
5. **Edit substitutions** if needed (device name, etc.)
6. **Compile and upload** via ESPHome dashboard

### Method 3: Git Submodule (Advanced)
```bash
# Add as submodule to your ESPHome configs
git submodule add https://github.com/ApolloAutomation/MTR-1.git mtr1
# Reference files using !include mtr1/Integrations/ESPHome/Core.yaml
```

## ⚙️ Customization

### Device Naming
Edit the substitutions in your chosen YAML file:
```yaml
substitutions:
  name: my-mtr1-bedroom  # Change this to your preferred name
  version: "25.4.11.1"
```

### Sensor Calibration
Access calibration controls in Home Assistant:
- **Temperature Offset**: Compensate for self-heating
- **CO2 Calibration**: Set reference point for accuracy
- **Motion Zones**: Configure detection areas

### Advanced Features
- **Buzzer Notifications**: Create audio alerts via Home Assistant services
- **RGB Status**: Customize LED colors for different states
- **Presence Zones**: Define multiple detection areas
- **Update Intervals**: Adjust sensor reading frequency for battery optimization

## 📊 Available Sensors

| Sensor Type | Measurement | Update Interval | Use Cases |
|-------------|-------------|-----------------|-----------|
| **Motion/Presence** | Multi-target tracking, zones | 500ms | Occupancy, security, automation triggers |
| **Temperature** | °C/°F (DPS310 & SCD40) | 30s/60s | Climate control, comfort monitoring |
| **Humidity** | % RH (SCD40) | 60s | Ventilation control, mold prevention |
| **Pressure** | hPa (DPS310) | 30s | Weather monitoring, altitude |
| **CO2** | ppm (SCD40) | 60s | Air quality, ventilation alerts |
| **Light** | Lux (LTR390) | 5s | Automatic lighting, circadian rhythm |
| **UV Index** | 0-11 scale (LTR390) | 5s | UV exposure monitoring |
| **System** | WiFi, uptime, temperature | 60s | Device health monitoring |

## 🔧 Troubleshooting

### Device Not Connecting to WiFi
1. **Reset device** - Hold button for 8+ seconds until LED turns red
2. **Check WiFi credentials** - Ensure 2.4GHz network compatibility
3. **Move closer to router** - Improve signal strength during setup

### Sensors Not Reading
1. **Check I2C connections** - Enable I2C scanning in logs
2. **Verify power supply** - Ensure stable 5V power
3. **Review calibration** - Reset temperature offsets if needed

### Home Assistant Integration Issues
1. **Check ESPHome logs** - Look for connection errors
2. **Restart ESPHome add-on** - Refresh integration
3. **Re-discover device** - Remove and re-add if necessary

## 📈 Recent Updates

- **v25.4.11.1**: Enhanced reliability with watchdog and safe mode
- **Improved WiFi**: Better connection handling and station mode support
- **Better Logging**: Enhanced debugging capabilities
- **Sensor Timeouts**: Protection against sensor failures
- **Documentation**: Comprehensive setup guides and troubleshooting

For detailed changelog, see [.github/copilot-updates.md](.github/copilot-updates.md)


## 🔗 Resources & Support

### Official Links
- **🛒 Shop**: [Apollo Automation Store](https://apolloautomation.com)
- **📚 Wiki**: [Comprehensive Documentation](https://wiki.apolloautomation.com)
- **💬 Discord**: [Community Support](https://dsc.gg/ApolloAutomation)
- **🎨 3D Files**: [Printable Cases & Mounts](https://www.printables.com/model/932043-apollo-automation-mtr-1-multi-target-radar-multise)

### Technical Resources
- **📖 ESPHome Documentation**: [Official ESPHome Docs](https://esphome.io/)
- **🏠 Home Assistant**: [Integration Guide](https://www.home-assistant.io/integrations/esphome/)
- **📋 Hardware Specs**: See `/Datasheets/` folder in this repository
- **🔧 API Reference**: Built-in web server at `http://[device-ip]`

### Community & Feedback
- **🐛 Bug Reports**: [GitHub Issues](https://github.com/ApolloAutomation/MTR-1/issues)
- **💡 Feature Requests**: Discord community or GitHub discussions
- **🤝 Contributions**: Pull requests welcome for improvements
- **📱 Support**: Discord server for fastest community response

---

**Made with ❤️ by Apollo Automation** | *Bringing smart sensors to everyone*
