cmake_minimum_required (VERSION 3.17.0)
project (SdBusPlus VERSION 1.0.0 DESCRIPTION "mylib description")

set (WANT_TRANSACTION "0" CACHE STRING
     "The max HTTP request body size in MB")

set(SDBUSPLUS_LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/sdbusplus")

configure_file(${SDBUSPLUS_LIB_DIR}/bus.hpp.in ${SDBUSPLUS_LIB_DIR}/bus.hpp)
configure_file(${SDBUSPLUS_LIB_DIR}/server.hpp.in ${SDBUSPLUS_LIB_DIR}/server.hpp)

set (SDBUSPLUS_SRC_FILES ${SDBUSPLUS_LIB_DIR}/exception.cpp ${SDBUSPLUS_LIB_DIR}/sdbus.cpp)

add_library (sdbusplus SHARED ${SDBUSPLUS_SRC_FILES})


target_include_directories(sdbusplus PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

set_target_properties(sdbusplus PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
    PUBLIC_HEADER ${SDBUSPLUS_LIB_DIR}/asio/connection.hpp)

set(PREFIX ${CMAKE_INSTALL_PREFIX})
configure_file(sdbusplus.pc.in sdbusplus.pc @ONLY)