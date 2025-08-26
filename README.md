# PUMP-1 Smart Pump Controller

![Apollo Automation Logo](https://github.com/jadehawk/IconsBackup/blob/main/Icons/apollo-automations-logo.png)

An ESPHome-based intelligent pump controller with advanced safety features, water level monitoring, and flexible control options. The PUMP-1 is designed for reliable water management in various applications including drainage, filling, and automated irrigation systems.

## 🌟 Features

### Core Functionality
- **Smart Pump Control**: GPIO-based pump control with multiple activation methods
- **Water Level Detection**: Built-in water sensor monitoring with configurable logic
- **Configurable Run Time**: Adjustable pump duration from 1 to 300 seconds
- **Safety Overrides**: Manual override options for water protection and pump safety

### Safety Features
- **Water Detection Safety**: Prevents pump operation when no water is detected (configurable)
- **Runtime Protection**: Configurable maximum safe runtime with automatic alerts
- **Inverted Logic Mode**: Support for tank filling applications (stops when water is detected)
- **Visual & Audio Alerts**: RGB LED and buzzer notifications for system status and warnings

### Control Methods
1. **Home Assistant Integration**: Full control via Home Assistant dashboard
2. **Web Interface**: Built-in web server for local control
3. **Physical Button**: Quick pump activation via reset button tap
4. **API Services**: Programmatic control through ESPHome API
5. **Manual Switch**: Direct pump control toggle

### Monitoring & Alerts
- **Hourly Water Check**: Automatic water level monitoring with audible alerts
- **Runtime Monitoring**: Real-time pump operation tracking
- **Safety Alerts**: Visual (RGB LED) and audio (buzzer) warnings for extended runtime
- **Status Indicators**: RGB LED shows connection status (WiFi, Home Assistant)

## 🔧 Hardware Requirements

### Compatible Board
- **ESP32-C6-DevKitM-1** (8MB Flash)
- ESP-IDF framework

### Pin Configuration
| Component | GPIO Pin | Description |
|-----------|----------|-------------|
| Pump Relay | GPIO7 | Controls pump power |
| Water Sensor | GPIO4 | Detects water presence |
| Reset Button | GPIO9 | Multi-function button |
| RGB LED | GPIO3 | WS2812 status indicator |
| Buzzer | GPIO10 | Audio feedback |

### Additional Hardware
- 5V/12V/24V relay module (depending on pump voltage)
- Water level sensor (float switch or conductivity sensor)
- Optional: External power supply for pump

## ⚙️ Configuration Options

### Basic Settings

| Setting | Default | Range | Description |
|---------|---------|-------|-------------|
| Pump Run Seconds | 10s | 1-300s | Default pump runtime |
| Max Safe Run Time | 120s | 30-600s | Maximum runtime before safety alert |
| Hourly Water Check | ON | ON/OFF | Enable hourly water monitoring |
| Invert Water Logic | OFF | ON/OFF | Reverse water detection logic |

## 📱 Usage Examples

### Home Assistant Automation
```yaml
automation:
  - alias: "Daily Garden Watering"
    trigger:
      - platform: time
        at: "06:00:00"
    action:
      - service: esphome.apollo_pump_1_run_pump_for_seconds
        data:
          seconds: 60
```

### API Service Call
```yaml
# Run pump for specific duration
service: esphome.apollo_pump_1_run_pump_for_seconds
data:
  seconds: 30
```

### Physical Button Control
- **Single tap**: Run pump for configured duration
- **Hold 10+ seconds**: Factory reset device

## 🔌 API Documentation

### Available Services

#### `run_pump_for_seconds`
Runs the pump for a specified duration.
- **Parameter**: `seconds` (integer, 1-300)
- **Example**: `{"seconds": 45}`

#### `play_buzzer`
Plays a custom RTTTL melody.
- **Parameter**: `song_str` (string, RTTTL format)
- **Example**: `{"song_str": "beep:d=4,o=5,b=200:c,p,c"}`

### Sensors & Switches

| Entity | Type | Description |
|--------|------|-------------|
| `pump_control` | Switch | Main pump control |
| `water_exists` | Binary Sensor | Water detection status |
| `pump_run_seconds` | Number | Configurable runtime |
| `water_protection_override` | Switch | Bypass water safety |
| `hourly_water_check_enabled` | Switch | Enable hourly monitoring |
| `invert_water_logic` | Switch | Reverse water logic |

## 🛡️ Safety Features

### Water Detection Safety
The pump will only operate when water is detected (unless overridden). This prevents dry running and pump damage.

### Runtime Protection
If the pump runs longer than the configured maximum safe time:
1. Audio alert plays
2. RGB LED flashes red
3. Pump continues running (unless safety override is disabled)

### Inverted Logic Mode
For tank filling applications:
- Pump runs when water is NOT detected
- Automatically stops when water reaches sensor
- Completion melody plays

## 🔧 Troubleshooting

### Common Issues

| Problem | Solution |
|---------|----------|
| Pump won't start | Check water sensor, verify override settings |
| No WiFi connection | Check credentials, ensure 2.4GHz network |
| Factory reset needed | Hold button for 10+ seconds |
| Water sensor inverted | Toggle "Invert Water Logic" switch |

### LED Status Indicators
- **Blue**: Connected to Home Assistant
- **Green**: Connected to WiFi only
- **Yellow**: No WiFi connection
- **Red (flashing)**: Safety alert active

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](License.md) file for details.

## 🏢 About Apollo Automation

Apollo Automation creates innovative smart home devices that seamlessly integrate with Home Assistant and ESPHome. Visit our [website](https://apolloautomation.com) for more products and information.

## 📞 Support

For any issues or support needs, please contact us at:
- **Email**: [support@apolloautomation.com](mailto:support@apolloautomation.com)

Additional resources:
- **Documentation**: [Wiki](https://wiki.apolloautomation.com)
- **Discord Community**: [Join our community](https://discord.gg/apolloautomation)

---

Made with ❤️ by Apollo Automation
