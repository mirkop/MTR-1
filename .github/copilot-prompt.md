# GitHub Copilot Project Context - Apollo MTR-1

## Project Overview

The Apollo MTR-1 is an advanced multi-sensor IoT device built on the ESP32-C3 platform, designed for comprehensive room monitoring in Home Assistant environments. This project provides ESPHome configurations for a device that combines motion detection, environmental monitoring, and presence sensing capabilities.

## Technology Stack

- **Platform**: ESP32-C3 microcontroller
- **Framework**: ESPHome (minimum version 2024.6.4)
- **Integration**: Home Assistant via ESPHome
- **Communication**: WiFi, optional Bluetooth Low Energy (BLE)
- **Programming Language**: YAML configuration files with embedded C++ lambda functions

## Hardware Components

### Sensors
- **LD2450 Radar**: Multi-target motion and presence detection via UART
- **SCD40**: CO2, temperature, and humidity sensor via I2C
- **DPS310**: Atmospheric pressure and temperature sensor via I2C
- **LTR390**: Light and UV index sensor via I2C

### Interfaces
- **I2C Bus**: GPIO1 (SDA), GPIO0 (SCL) at 100kHz
- **UART**: GPIO21 (TX), GPIO20 (RX) at 256000 baud for LD2450
- **RGB LED Strip**: GPIO3 (WS2812, 3 LEDs, GRB order)
- **Buzzer**: GPIO10 (LEDC PWM output for RTTTL)
- **Button**: GPIO9 (pullup, inverted, factory reset functionality)

## Project Structure

```
/
├── Integrations/ESPHome/
│   ├── Core.yaml              # Shared sensor and component definitions
│   ├── MTR-1.yaml            # Standard configuration (recommended)
│   ├── MTR-1_BLE.yaml        # Bluetooth proxy variant
│   └── MTR-1_Factory.yaml    # Factory firmware with ESP32 Improv
├── Datasheets/               # Hardware component specifications
├── static/                   # Web assets
├── .github/
│   ├── copilot-updates.md    # Change log and improvements
│   └── copilot-prompt.md     # This file
├── README.md                 # User documentation
└── License.md
```

## Code Patterns and Conventions

### ESPHome Configuration Style
- Use descriptive names with underscores: `dps310_temperature_offset`
- Include comments for calibration values and hardware-specific settings
- Maintain consistent indentation (2 spaces)
- Group related components logically
- Use entity categories: `CONFIG`, `DIAGNOSTIC`

### Sensor Configuration Standards
- Include timeout filters for reliability: `timeout: 120s`
- Add meaningful descriptions and units
- Use appropriate update intervals based on sensor type
- Implement error handling and fallback values

### Lambda Functions
- Use consistent variable naming: `id(sensor_name).state`
- Include bounds checking for sensor values
- Comment complex calculations
- Handle NaN and invalid readings gracefully

## Key Design Principles

### Reliability
- Watchdog timer enabled for system stability
- Safe mode configuration for automatic recovery
- Sensor timeout protection to prevent hangs
- I2C bus scanning for diagnostic purposes

### User Experience
- Clear entity naming for Home Assistant integration
- Appropriate default values for calibration
- Status indicators via RGB LED
- Audio feedback via buzzer for important events

### Maintainability
- Shared `Core.yaml` for consistency across variants
- Well-documented configuration options
- Version control for firmware updates
- Comprehensive testing scripts for factory validation

## Common Tasks and Patterns

### Adding New Sensors
1. Define hardware interface (I2C/SPI/GPIO)
2. Add sensor platform configuration
3. Include appropriate filters and error handling
4. Add to factory test script if applicable
5. Update documentation and entity descriptions

### Calibration Implementation
```yaml
- platform: template
  name: "Sensor Calibration Offset"
  id: sensor_offset
  restore_value: true
  initial_value: 0.0  # Default calibration value
  entity_category: "CONFIG"
  # ... other template sensor properties
```

### Service Definitions
```yaml
api:
  services:
    - service: custom_action
      variables:
        parameter: string
      then:
        - lambda: "// Custom action implementation"
```

### Factory Testing Patterns
- Use global variables for test state tracking
- Implement timeout-based test cycles
- Provide visual feedback via RGB LED
- Include sensor validation ranges

## Integration Guidelines

### Home Assistant Entities
- Use descriptive friendly names
- Set appropriate device classes and units
- Configure entity categories for organization
- Disable diagnostic entities by default

### ESPHome Best Practices
- Minimize memory usage with appropriate update intervals
- Use substitutions for commonly changed values
- Implement proper error handling for network issues
- Include OTA update mechanisms

## Security Considerations

- Factory firmware includes ESP32 Improv for secure setup
- Production configs should use encrypted OTA updates
- WiFi credentials handled via captive portal
- Consider implementing device authentication for sensitive applications

## Testing and Validation

### Factory Test Script
The `testScript` validates all sensors by:
1. Checking sensor readings within expected ranges
2. Providing visual feedback via RGB LED
3. Cycling through multiple test iterations
4. Resetting on button press

### Recommended Testing
- Verify all sensor readings in different environments
- Test WiFi connectivity and reconnection
- Validate OTA update functionality
- Check factory reset procedures

## Documentation Standards

### Code Comments
- Explain calibration requirements and typical values
- Document hardware-specific configurations
- Include troubleshooting notes for common issues
- Reference relevant datasheets or specifications

### User Documentation
- Provide clear setup instructions
- Include troubleshooting guides
- Document all available services and entities
- Maintain version history and changelogs

## Future Development Guidelines

### Adding Features
- Maintain backward compatibility
- Update all configuration variants consistently
- Include comprehensive testing
- Document changes in copilot-updates.md

### Performance Optimization
- Monitor memory usage during development
- Optimize sensor update intervals
- Consider power management for battery scenarios
- Implement efficient data structures for multi-target tracking

---

This context helps GitHub Copilot understand the project structure, coding patterns, and design principles when providing suggestions and generating code for the Apollo MTR-1 ESPHome project.
