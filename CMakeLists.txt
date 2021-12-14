cmake_minimum_required(VERSION 3.13)

set(esp_idf_dir "${CMAKE_CURRENT_LIST_DIR}/freertos/vendors/espressif/esp-idf")
include(${esp_idf_dir}/tools/cmake/idf.cmake)
string(FIND "${CMAKE_TOOLCHAIN_FILE}" "esp32" SOC_TOOLCHAIN_ESP32)
set(SOC_NAME "esp32")

project(my_app)

#add_executable(my_app src/main.c)

# Tell IDF build to link against this target.
set(IDF_PROJECT_EXECUTABLE my_app)
get_filename_component(
    IDF_EXECUTABLE_SRCS
    "src/main.c" ABSOLUTE
    )

# Add freertos as an subdirectory. AFR_BOARD tells which board to target.
if("${SOC_NAME}" STREQUAL "esp32")
    set(AFR_BOARD espressif.esp32_devkitc CACHE INTERNAL "")
else()
    message( FATAL_ERROR "Unsupported SOC" )
endif()
add_subdirectory(freertos)

# Link against the mqtt library so that we can use it. Dependencies are transitively
# linked.
target_link_libraries(
    ${IDF_PROJECT_EXECUTABLE} 
    PRIVATE 
    AFR::freertos
) 