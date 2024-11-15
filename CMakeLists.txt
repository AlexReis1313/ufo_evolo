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