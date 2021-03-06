#=============================================================================#
# Author: Konstantin Gredeskoul https://github.com/kigster                    #
# © 2017 All rights reserved, MIT License                                     #
#                                                                             #
# Description: Arduino CMake Top Level file that uses Arli Library Manager    #
# https://github.com/kigster/arli                                             #
#                                                                             #
# Depends on Arduino-CMake project found at                                   #
# https://github.com/arduino-cmake/arduino-cmake                              #
#                                                                             #
#=============================================================================#

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
set(CMAKE_LOCAL_DIR ${CMAKE_CURRENT_SOURCE_DIR}/cmake/)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(ARDUINO_SDK_PATH /Applications/Arduino.app/Contents/Java)

include(Arli)

arli_setup(${CMAKE_CURRENT_SOURCE_DIR})

# These flags are required to ensure that the resulting binary is as small is it can be.
# See: https://github.com/arduino-cmake/arduino-cmake/issues/67 for more info.
set(ARDUINO_CXX_FLAGS "-w -g -std=c++11 -fpermissive -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics")
set(ARDUINO_LINKER_FLAGS "-w -g -fuse-linker-plugin -Wl,--gc-sections")

set(CMAKE_TOOLCHAIN_FILE cmake/ArduinoToolchain.cmake)

cmake_minimum_required(VERSION 2.8)
project(BattleShift C CXX ASM)

add_subdirectory(src)
