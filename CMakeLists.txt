cmake_minimum_required(VERSION 3.16...3.24)

# The default build type must be set before project()
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR AND NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()

project(UFO
	VERSION 1.0.0
	DESCRIPTION "UFO"
	LANGUAGES CXX C
)

option(UFO_TESTING  "Unit testing"                       OFF)
option(UFO_COVERAGE "Test Coverage"                      OFF)
option(UFO_DEV_MODE "Set up development helper settings" ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
# set(CMAKE_CXX_CLANG_TIDY clang-tidy)

set(UFO_SUPER_BUILD ON)

add_subdirectory(cloud)
add_subdirectory(compute)
add_subdirectory(container)
add_subdirectory(core)
add_subdirectory(geometry)
add_subdirectory(map)
add_subdirectory(math)
add_subdirectory(morton)
add_subdirectory(plan)
add_subdirectory(time)
add_subdirectory(utility)
add_subdirectory(vision)

include(GNUInstallDirs)

include(CMakePackageConfigHelpers)
configure_package_config_file(
	"${CMAKE_CURRENT_SOURCE_DIR}/cmake/ufo-config.cmake.in"
	"${CMAKE_CURRENT_BINARY_DIR}/ufo-config.cmake"
	INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)

write_basic_package_version_file(
	"${CMAKE_CURRENT_BINARY_DIR}/ufo-config-version.cmake"
	VERSION ${PROJECT_VERSION}
	COMPATIBILITY SameMajorVersion
)

INSTALL(
	FILES
		"${CMAKE_CURRENT_BINARY_DIR}/ufo-config.cmake"
		"${CMAKE_CURRENT_BINARY_DIR}/ufo-config-version.cmake"
	DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)