idf_component_register(
    SRCS "smbus.c"  # list your .c files
    INCLUDE_DIRS "include"
    REQUIRES driver
)