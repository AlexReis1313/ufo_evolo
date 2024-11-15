cmake_minimum_required(VERSION 3.5...3.16)

project(
	ufo
	VERSION 1.0.0
	DESCRIPTION "UFO"
	LANGUAGES CXX C
)

option(UFO_TESTING  "Unit testing"                       OFF)
option(UFO_COVERAGE "Test Coverage"                      OFF)
option(UFO_DEV_MODE "Set up development helper settings" ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
# set(CMAKE_CXX_CLANG_TIDY clang-tidy)

set(UFO_COMPONENT_MODE ON)

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

configure_file(${project}-config.cmake
  "${CMAKE_BINARY_DIR}/${project}-config.cmake"
  @ONLY
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_BINARY_DIR}/${project}-config-version.cmake"
  VERSION ${version}
  COMPATIBILITY AnyNewerVersion
)

install(
  FILES
    "${CMAKE_BINARY_DIR}/${project}-config.cmake"
  DESTINATION lib/cmake/${project}
)