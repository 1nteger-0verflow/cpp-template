cmake_minimum_required(VERSION 3.15...3.26)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(sample LANGUAGES CXX)

# guard against in-source builds
if(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
    message(
        FATAL_ERROR
        "In-source builds not allowed. Please make a new directory (called a build directory) and run CMake from there. You may need to remove CMakeCache.txt. "
    )
endif()

add_executable(sample src/main.cpp)

target_include_directories(sample PRIVATE include)

target_compile_features(sample PRIVATE cxx_std_17)
target_compile_options(
    sample
    PRIVATE
        -Wall
        -Wfatal-errors
        -Wundef
        -fPIC
        $<$<CONFIG:Release>:
        -O3>
        $<$<CONFIG:Debug>:
        -O0
        -fstandalone-debug>
)

