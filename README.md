# ESPHome LVGL Dual Heat-Cool Thermostat

This repository contains an ESPHome configuration for a dual heat-cool thermostat running on the Guition ESP32-S3-4848S040 smart display. The interface closely follows the Home Assistant thermostat layout and design.

## 📱 Hardware Specifications
**Guition ESP32-S3-4848S040**

- **Display**: ST7701S - 4 inch, 480 × 480 pixels IPS touchscreen
- **MCU**: ESP32-S3 dual-core processor with 8MB PSRAM
- **Touch**: GT911 capacitive touch controller
- **Connectivity**: Wi-Fi 802.11 b/g/n
- **Form Factor**: Wall-mountable smart display

## 🌡️ Thermostat Features

- **Dual Mode Operation**: Full heat-cool thermostat functionality
- **Home Assistant UI**: Interface design closely matches HA thermostat
- **Smart Preset System**: Intelligent preset management with visual indicators
- **Real-time Control**: Direct integration with Home Assistant climate entities
- **Touch Interface**: Responsive controls for temperature adjustment
- **Multiple Modes**: Heat, Cool, Heat-Cool, and Off modes with proper visual feedback
- **Vacation Mode**: Manual temperature control when presets are disabled
- **Auto-Recovery**: Robust handling of HA server and display restarts

## 🚧 Project Status
**Current Status**: Near-final release - Fully functional with latest updates

✅ **Heat-Cool mode fully functional and stable**  
✅ **Enhanced OFF mode with proper visual styling**  
✅ **Smart preset indicator system implemented**  
✅ **Vacation/manual mode functionality**  
✅ **Auto-restart recovery mechanisms**  
✅ **Bug fixes for HA server and display restarts**  
🔄 **Preset page redesign coming in final version**  
🔄 **Minor features planned for final release**  

## 🎯 Latest Updates (Pre-Final Version)

### Enhanced OFF Mode Behavior
- **Visual Feedback**: All interface elements turn gray when OFF mode is selected
- **Smart Highlighting**: Selected temperature values remain white for easy identification
- **Consistent Styling**: Unified color management across all interface components

### Smart Preset Indicator System
- **Visual Status**: Top-left corner icon shows current preset status
  - 🏠 **Home preset** (orange when active)
  - 🚗 **Away preset** (blue when active) 
  - 😴 **Sleep preset** (purple when active)
  - ⚙️ **Custom** (gray for manual adjustments)
  - 🌴 **Vacation mode** (green when presets disabled)

### Vacation/Manual Mode
- **Purpose**: Designed for vacations, irregular schedules, or manual control periods
- **Function**: When presets are disabled, thermostat maintains current temperatures until manually changed
- **Icon**: Palm tree symbol representing vacation/break from routine
- **Use Cases**: Winter/summer vacations, irregular work schedules, temporary manual control

### Improved Stability
- **Auto-Recovery**: Robust handling when HA server restarts
- **Display Recovery**: Proper arc and color restoration after LVGL display restarts
- **Bug Fixes**: Resolved temperature synchronization issues during system restarts

## 🔮 Coming in Final Version

The next update will be the **final release** featuring:
- **Redesigned Preset Page**: Elegant arc-based time setting interface
- **Simplified Navigation**: Single button toggle between thermostat and preset pages
- **Code Optimization**: Organized and optimized codebase
- **Additional Features**: Display timeout, screensaver with clock/weather
- **Complete Documentation**: Comprehensive setup and customization guide

*Note: The current preset page will be completely redesigned. The existing slider-based interface will be replaced with an elegant arc-based solution integrated into the main thermostat interface.*

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

**Important**: Edit the code to match your temperature sensor! (from line #639 to #642)
```yaml
sensor:
  - platform: homeassistant
    id: ble_sensor_raw
    entity_id: sensor.temperature_sensor_1_temperature  # Change this to your sensor
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

### Main Interface
- **Heat-Cool Mode**: Fully functional - recommended mode for complete feature testing
- **Temperature Control**: Touch interface for precise temperature adjustment
- **Mode Selection**: Switch between Heat, Cool, Heat-Cool, and Off modes
- **Preset Indicator**: Visual feedback for current preset status in top-left corner

### Preset System
- **Automatic Mode**: When enabled, follows daily schedule (Home → Away → Sleep cycle)
- **Vacation Mode**: When disabled, maintains current temperatures manually
- **Visual Feedback**: Icon changes based on active preset or manual mode

### Controls
- **Arc Interface**: Drag to adjust target temperatures
- **+/- Buttons**: Fine temperature adjustments (0.1°C increments)
- **Mode Buttons**: Heat/Cool/Auto/Off selection with proper visual feedback
- **Preset Toggle**: Access preset configuration (current interface, redesign coming)

## 🏠 Home Assistant Integration

The thermostat integrates seamlessly with Home Assistant:
- Appears as a climate entity
- Real-time temperature and humidity display
- Mode and temperature control from both HA and display
- Preset management and synchronization
- Robust recovery from server restarts

## 🔧 Troubleshooting

### Common Issues
- **Missing fonts**: Download and place required fonts in `fonts/` directory
- **Images not displaying**: Ensure PNG files are copied to ESPHome `images/` folder
- **Colors not working**: Verify `colors.h` is in ESPHome root directory
- **Wi-Fi connection issues**: Check credentials in `secrets.yaml`
- **Temperature sync issues**: Verify your temperature sensor entity ID is correct

### Recovery Features
- **Automatic Recovery**: System automatically recovers from HA server restarts
- **Display Recovery**: Interface properly restores after LVGL restarts
- **Temperature Sync**: Maintains temperature settings during system restarts

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⚠️ Disclaimer

This project is not affiliated with Guition or Espressif. Use at your own risk. Always verify pin configurations before uploading to prevent hardware damage.

---

**Happy building! 🎉**

*If you find this project helpful, please give it a ⭐ on GitHub!*

---

### 🔄 Version History
- **Current**: Pre-final release with enhanced OFF mode, smart presets, and stability improvements
- **Next**: Final release with redesigned preset interface and additional features
