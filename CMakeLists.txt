cmake_minimum_required(VERSION 3.8)
#set(CMAKE_CXX_COMPILER "/usr/bin/c++")

project(financial)


# ============================================================
# Set the Standard version.

include(CheckCXXCompilerFlag)

check_cxx_compiler_flag("-std=c++14" COMPILER_SUPPORTS_CXX14)
check_cxx_compiler_flag("-std=c++11" COMPILER_SUPPORTS_CXX11)
check_cxx_compiler_flag("-std=c++0x" COMPILER_SUPPORTS_CXX0X)

if (COMPILER_SUPPORTS_CXX14)
    add_definitions(-std=c++14)
elseif (COMPILER_SUPPORTS_CXX11)
    add_definitions(-std=c++11)
elseif (COMPILER_SUPPORTS_CXX0X)
    add_definitions(-std=c++0x)
else ()
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif ()

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_VERBOSE_MAKEFILE 1)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# -Werror
# for boost: -O2 -fno-exceptions -fno-rtti
set(CMAKE_CXX_FLAGS "-O2 -fno-exceptions -fno-rtti -Wall -Wextra -Werror -pedantic -pedantic-errors -pipe")
set(CMAKE_EXE_LINKER_FLAGS "-pthread")
set(GCC_OPTIMIZATIONS "")

# -lstdc++fs - for safe keeping (--enable-libstdcxx-filesystem-ts)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_OPTIMIZATIONS}")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS}")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/build")

file(GLOB SOURCE_FILES Black-Scholes/Black_Scholes.cpp)
add_executable(cpp-financial ${SOURCE_FILES})