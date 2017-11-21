
cmake_minimum_required (VERSION 3.8.2) 
project(CMakeBug)

set(CMAKE_VERBOSE_MAKEFILE ON)
if( (NOT ${CMAKE_GENERATOR} MATCHES "Unix Makefiles") AND ( NOT CMAKE_COMPILER_IS_GNUCXX ))
    message(FATAL_ERROR "Example requires gcc and \"Unix Makefiles\"" )
endif()

add_library( libFoo INTERFACE )
target_compile_options( libFoo INTERFACE -include "${CMAKE_CURRENT_SOURCE_DIR}/foo.h" )

add_executable( bar main.cpp bar.h)
target_compile_options( bar PRIVATE -include "${CMAKE_CURRENT_SOURCE_DIR}/bar.h" )

target_link_libraries( bar PUBLIC libFoo )
