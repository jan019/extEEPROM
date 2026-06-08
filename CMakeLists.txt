# v3.21 implemented semantic changes regarding $<TARGET_OBJECTS:...>
# See https://cmake.org/cmake/help/v3.21/command/target_link_libraries.html#linking-object-libraries-via-target-objects
cmake_minimum_required(VERSION 3.21)

add_library(extEEPROM INTERFACE)
add_library(extEEPROM_usage INTERFACE)

target_include_directories(extEEPROM_usage INTERFACE
  .
)


target_link_libraries(extEEPROM_usage INTERFACE
  base_config
  Wire
)

target_link_libraries(extEEPROM INTERFACE extEEPROM_usage)



add_library(extEEPROM_bin OBJECT EXCLUDE_FROM_ALL
  extEEPROM.cpp
)
target_link_libraries(extEEPROM_bin PUBLIC extEEPROM_usage)

target_link_libraries(extEEPROM INTERFACE
  extEEPROM_bin
  $<TARGET_OBJECTS:extEEPROM_bin>
)

