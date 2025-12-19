idf_component_register(
    SRCS "i2c-lcd1602.c"  # list your .c files
    INCLUDE_DIRS "include"
    REQUIRES driver esp32-smbus
)
