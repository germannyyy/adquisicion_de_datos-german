# Set CMake minimum version
cmake_minimum_required(VERSION 3.13)

# Pull in SDK (must be before project)
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Set project name
project(main C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# SDK version error message
if (PICO_SDK_VERSION_STRING VERSION_LESS "1.3.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.3.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

# Initialize Pico SDK
pico_sdk_init()

# File to output
add_executable(${PROJECT_NAME}
    main.c
)

# Enable/disable stdio output
pico_enable_stdio_usb(${PROJECT_NAME} 1)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

# Link libraries with main project
target_link_libraries(${PROJECT_NAME}
    pico_stdlib
    hardware_adc
)
pico_add_extra_outputs(${PROJECT_NAME})
