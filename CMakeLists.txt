cmake_minimum_required (VERSION 3.0)
project(netcode C CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED on)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

include_directories(${CMAKE_CURRENT_LIST_DIR})

set(sodium_USE_STATIC_LIBS ON)

include(FindSodium)
if(NOT sodium_FOUND)
  FIND_LIBRARY(sodium_LIBRARY_DEBUG libsodium sodium-debug.lib PATHS "./windows" DOC "Sodium debug library")
  FIND_LIBRARY(sodium_LIBRARY_RELEASE libsodium sodium-release.lib PATHS "./windows" DOC "Sodium release library")
  FIND_PATH(sodium_INCLUDE_DIR sodium.h "./windows" DOC "Sodium includes")
endif(NOT sodium_FOUND)

include_directories(${sodium_INCLUDE_DIR})

add_library(netcode "netcode.c" "netcode.h")

target_link_libraries(netcode ${sodium_LIBRARY_RELEASE})