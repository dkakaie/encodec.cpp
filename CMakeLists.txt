cmake_minimum_required(VERSION 3.12)
project("encodec.cpp" C CXX)

if (NOT XCODE AND NOT MSVC AND NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    set(ENCODEC_STANDALONE ON)
else()
    set(ENCODEC_STANDALONE OFF)
endif()

# Build libraries

set(ENCODEC_LIB encodec.cpp)

add_library(
        ${ENCODEC_LIB}
        encodec
        encodec.cpp
        encodec.h
)

target_link_libraries(${ENCODEC_LIB} PUBLIC ggml)
target_include_directories(${ENCODEC_LIB} PUBLIC .)
target_compile_features(${ENCODEC_LIB} PUBLIC cxx_std_11)