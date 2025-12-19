idf_component_register(
    SRCS "app_main.c"
    INCLUDE_DIRS "."
    REQUIRES driver esp32-i2c-lcd1602 esp32-smbus
    PRIV_REQUIRES esp_driver_gpio  # Add this for ESP-IDF v5.x+
)
