# This file is automatically generated from cmake.toml - DO NOT EDIT
# See https://github.com/build-cpp/cmkr for more information

cmake_minimum_required(VERSION 3.15)

# Regenerate CMakeLists.txt automatically in the root project
set(CMKR_ROOT_PROJECT OFF)
if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
	set(CMKR_ROOT_PROJECT ON)

	# Bootstrap cmkr
	include(cmkr.cmake OPTIONAL RESULT_VARIABLE CMKR_INCLUDE_RESULT)
	if(CMKR_INCLUDE_RESULT)
		cmkr()
	endif()

	# Enable folder support
	set_property(GLOBAL PROPERTY USE_FOLDERS ON)
endif()

# Create a configure-time dependency on cmake.toml to improve IDE support
if(CMKR_ROOT_PROJECT)
	configure_file(cmake.toml cmake.toml COPYONLY)
endif()

project(vmemu)

# deps
set(CMKR_CMAKE_FOLDER ${CMAKE_FOLDER})
if(CMAKE_FOLDER)
	set(CMAKE_FOLDER "${CMAKE_FOLDER}/deps")
else()
	set(CMAKE_FOLDER deps)
endif()
add_subdirectory(deps)
set(CMAKE_FOLDER ${CMKR_CMAKE_FOLDER})

# tools
set(CMKR_CMAKE_FOLDER ${CMAKE_FOLDER})
if(CMAKE_FOLDER)
	set(CMAKE_FOLDER "${CMAKE_FOLDER}/tools")
else()
	set(CMAKE_FOLDER tools)
endif()
add_subdirectory(tools)
set(CMAKE_FOLDER ${CMKR_CMAKE_FOLDER})

# Target vmemu
set(CMKR_TARGET vmemu)
set(vmemu_SOURCES "")

list(APPEND vmemu_SOURCES
	"src/vmemu_t.cpp"
	"include/vmemu_t.hpp"
)

list(APPEND vmemu_SOURCES
	cmake.toml
)

set(CMKR_SOURCES ${vmemu_SOURCES})
add_library(vmemu STATIC)

if(vmemu_SOURCES)
	target_sources(vmemu PRIVATE ${vmemu_SOURCES})
endif()

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${vmemu_SOURCES})

target_compile_definitions(vmemu PUBLIC
	NOMINMAX
)

target_compile_features(vmemu PUBLIC
	cxx_std_20
)

target_include_directories(vmemu PUBLIC
	include
)

target_link_libraries(vmemu PUBLIC
	vmprofiler
	unicorn
	cli-parser
)

unset(CMKR_TARGET)
unset(CMKR_SOURCES)

