cmake_minimum_required(VERSION 3.16)

project(TelemetryBoard LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
pkg_check_modules(MOSQUITTO REQUIRED IMPORTED_TARGET libmosquitto)

add_executable(TelemetryBoard
        src/main.c
        src/sensors/mock_sensors.c
        src/mqtt_client.c
        src/processing.c
)

target_include_directories(TelemetryBoard PRIVATE
        ${PROJECT_SOURCE_DIR}/include
)

target_link_libraries(TelemetryBoard PRIVATE
        PkgConfig::MOSQUITTO
        m
)