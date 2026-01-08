# EMBEDDER.md - Project Configuration

## Project Overview
- **Name:** esp32-i2c-lcd1602-example
- **Description:** Example application for HD44780-compatible LCD1602 display via I2C backpack on ESP32
- **Platform:** ESP32 (Xtensa LX6)
- **Framework:** ESP-IDF v3.3+
- **Build System:** CMake / idf.py

## Hardware Configuration

### MCU
- **Chip:** ESP32-DevKit-V1
- **Core:** Dual-core Xtensa LX6 @ 240 MHz
- **Flash:** 4 MB
- **RAM:** 520 KB SRAM

### Peripherals
| Peripheral | Type | Interface | Pins | Address/Config |
|------------|------|-----------|------|----------------|
| LCD1602 | 16x2 Character LCD | I2C | SDA=GPIO18, SCL=GPIO19 | 0x27 |

### I2C Configuration
- **Port:** I2C_NUM_0
- **Speed:** 100 kHz (Standard Mode)
- **SDA:** GPIO 18 (configurable via Kconfig)
- **SCL:** GPIO 19 (configurable via Kconfig)
- **Pull-ups:** External (disabled in software)

## Build Commands
```bash
# Configure (optional - uses sdkconfig.defaults)
idf.py menuconfig

# Build
idf.py build

# Flash and monitor (hardware only)
idf.py -p /dev/ttyUSB0 flash monitor

# Clean build
idf.py fullclean
```

## Simulation
- **Simulator:** Wokwi
- **Config File:** wokwi.toml
- **Diagram:** diagram.json
- **Firmware Path:** build/esp32-i2c-lcd1602-example.bin
- **ELF Path:** build/esp32-i2c-lcd1602-example.elf

## Project Structure
```
/home/sandbox/workspace/
├── main/
│   ├── app_main.c           # Main application
│   ├── Kconfig.projbuild    # I2C pin configuration
│   └── CMakeLists.txt       # Main component build
├── components/
│   ├── esp32-i2c-lcd1602/   # LCD1602 I2C driver
│   │   ├── i2c-lcd1602.c
│   │   └── include/i2c-lcd1602.h
│   └── esp32-smbus/         # SMBus I2C abstraction
│       ├── smbus.c
│       └── include/smbus.h
├── CMakeLists.txt           # Project CMake config
├── sdkconfig.defaults       # Default SDK config
├── diagram.json             # Wokwi simulation diagram
└── wokwi.toml               # Wokwi configuration
```

## Component Dependencies
```
app_main.c
    └── i2c-lcd1602 (LCD driver)
            └── esp32-smbus (I2C communication)
                    └── ESP-IDF i2c driver
```

## Key Defines (main/app_main.c)
| Define | Value | Description |
|--------|-------|-------------|
| LCD_NUM_ROWS | 2 | Display rows |
| LCD_NUM_COLUMNS | 32 | Total columns (including hidden) |
| LCD_NUM_VISIBLE_COLUMNS | 16 | Visible columns |
| I2C_MASTER_FREQ_HZ | 100000 | I2C clock frequency |
| USE_STDIN | defined | Wait for keypress between demo steps |

## Configurable Options (Kconfig)
- `CONFIG_I2C_MASTER_SCL` - SCL GPIO (default: 19)
- `CONFIG_I2C_MASTER_SDA` - SDA GPIO (default: 18)
- `CONFIG_LCD1602_I2C_ADDRESS` - I2C address (default: 0x27)

## Documentation References
- [HD44780 Datasheet](https://www.sparkfun.com/datasheets/LCD/HD44780.pdf)
- [ESP-IDF I2C Driver](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/i2c.html)
