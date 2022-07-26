cmake_minimum_required(VERSION 3.13)

set(esp_idf_dir "${CMAKE_CURRENT_LIST_DIR}/freertos/vendors/espressif/esp-idf")
include(${esp_idf_dir}/tools/cmake/idf.cmake)
string(FIND "${CMAKE_TOOLCHAIN_FILE}" "esp32" SOC_TOOLCHAIN_ESP32)
set(SOC_NAME "esp32")

project(unit-test-app)

# add_executable(my_app src/main.c)

# Tell IDF build to link against this target.
set(IDF_PROJECT_EXECUTABLE unit-test-app)
get_filename_component(
    IDF_EXECUTABLE_SRCS
    "src/main.c" ABSOLUTE
    )

idf_build_component("components/test_utils")


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
    # AFR::kernel
    # AFR::common
    # idf::unity
    idf::test_utils
    3rdparty::unity
    # idf::mbedtls
) 

# # unity - test framework
# if(EXISTS "${AFR_3RDPARTY_DIR}/unity")
#     afr_3rdparty_module(unity)
#     target_sources(
#         3rdparty::unity INTERFACE
#         "${AFR_3RDPARTY_DIR}/unity/src/unity.c"
#         "${AFR_3RDPARTY_DIR}/unity/src/unity.h"
#         "${AFR_3RDPARTY_DIR}/unity/src/unity_internals.h"
#         "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture.c"
#         "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture.h"
#         "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture_internals.h"
#         "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture_malloc_overrides.h"
#     )
#     target_include_directories(
#         3rdparty::unity INTERFACE
#         "${AFR_3RDPARTY_DIR}/unity/src"
#         "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src"
#     )
#     target_compile_definitions(3rdparty::unity INTERFACE UNITY_INCLUDE_CONFIG_H)
# endif()