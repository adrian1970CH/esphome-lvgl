# ESPHome LVGL Dual Heat-Cool Thermostat

This repository contains an ESPHome configuration for a **dual heat-cool thermostat** running on the **Guition ESP32-S3-4848S040** smart display. The interface closely follows the Home Assistant thermostat layout and design.

## 📱 Hardware Specifications

**Guition ESP32-S3-4848S040**
- **Display**: 4 inch, 480 × 480 pixels IPS touchscreen
- **MCU**: ESP32-S3 dual-core processor with 8MB PSRAM
- **Touch**: GT911 capacitive touch controller
- **Connectivity**: Wi-Fi 802.11 b/g/n
- **Form Factor**: Wall-mountable smart display

## 🌡️ Thermostat Features

- **Dual Mode Operation**: Full heat-cool thermostat functionality
- **Home Assistant UI**: Interface design closely matches HA thermostat
- **Temperature Presets**: Functional preset page (currently being redesigned)
- **Real-time Control**: Direct integration with Home Assistant climate entities
- **Touch Interface**: Responsive controls for temperature adjustment
- **Multiple Modes**: Heat, Cool, Heat-Cool, and Off modes

## 🚧 Project Status

**Current Status**: In active development
- ✅ Heat-Cool mode fully functional and testable
- ✅ Basic preset page working
- 🔄 Preset page redesign in progress
- 🔄 Additional features being added regularly

This project will be updated regularly as new features are implemented.

## 📋 Requirements

### Software
- **ESPHome**: Version 2023.12.0 or later (for LVGL support)
- **Home Assistant**: Any recent version with ESPHome integration
- **Python**: 3.9+ (for ESPHome installation)

### Development Environment
- ESPHome Dashboard (recommended)

## 🛠️ Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/adrian1970CH/esphome-lvgl.git
cd esphome-lvgl
```

### 2. Prepare Required Files

**Copy images to your ESPHome images folder:**
- Copy the 2 PNG files from the `images/` folder to your ESPHome `images/` directory

**Add required fonts to your ESPHome fonts folder:**
- `materialdesignicons-webfont.ttf`
- `Roboto-Regular.ttf`
*(These fonts are not included in the repository)*

**Copy color definitions:**
- Place `colors.h` file in your ESPHome root directory

### 3. Configure Secrets
```bash
cp secrets.yaml.example secrets.yaml
```

Edit `secrets.yaml` with your credentials:
```yaml
wifi_ssid: "YourWiFiNetwork"
wifi_password: "YourWiFiPassword"
ap_password: "YourAccessPointPassword"
api_encryption_key: "your-32-character-encryption-key"
ota_password: "your-ota-update-password"
```
Edit code to match your temperature sensor! (around #639 to #642 line numbers)
```yaml
sensor:
  - platform: homeassistant
    id: ble_sensor_raw
    entity_id: sensor.temperature_sensor_1_temperature
```

### 4. Install ESPHome
```bash
pip3 install esphome
```

### 5. Test the Thermostat
```bash
# Compile configuration
esphome compile Guition-S3-square-4-inch.yaml

# Upload to device (first time via USB)
esphome upload Guition-S3-square-4-inch.yaml

# Test in Heat-Cool mode for full functionality
```

## 📁 Project Structure

```
esphome-lvgl/
├── README.md                         # This file
├── secrets.yaml.example              # Template for secrets
├── secrets.yaml                      # Your actual secrets (not in git)
├── Guition-S3-square-4-inch.yaml     # Main thermostat configuration
├── colors.h                          # Color definitions (copy to ESPHome root)
├── images/                           # UI images (copy PNGs to your ESPHome images/)
│   ├── image1.png
│   └── image2.png
└── fonts/                            # Required fonts (not included)
    ├── materialdesignicons-webfont.ttf  # Download separately
    └── Roboto-Regular.ttf               # Download separately
```

## 🌡️ Usage

1. **Heat-Cool Mode**: Fully functional - best mode for testing all features
2. **Preset Page**: Currently functional but basic design
3. **Temperature Control**: Touch interface for setting target temperatures
4. **Mode Selection**: Switch between Heat, Cool, Heat-Cool, and Off modes

## 🏠 Home Assistant Integration

The thermostat integrates seamlessly with Home Assistant:
- Appears as a climate entity
- Real-time temperature and humidity display
- Mode and temperature control from both HA and display
- Preset management

## 🔧 Troubleshooting

### Common Issues
1. **Missing fonts**: Download and place required fonts in fonts/ directory
2. **Images not displaying**: Ensure PNG files are copied to ESPHome images/ folder
3. **Colors not working**: Verify colors.h is in ESPHome root directory
4. **Wi-Fi connection issues**: Check credentials in secrets.yaml

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This project is not affiliated with Guition or Espressif. Use at your own risk. Always verify pin configurations before uploading to prevent hardware damage.

---

**Happy building!** 🎉

If you find this project helpful, please give it a ⭐ on GitHub!
