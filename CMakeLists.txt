cmake_minimum_required(VERSION 3.3)

option(HUNTER_STATUS_DEBUG "Print debug info" ON)

set(
    CMAKE_TOOLCHAIN_FILE
    ${CMAKE_CURRENT_LIST_DIR}/toolchain.cmake
    CACHE
    FILEPATH
    "Default toolchain"
)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.60.tar.gz"
    SHA1 "35a23a3e2f8a2c87f6762c43f3cc64a0bee50943"
)

project(curl-example)

hunter_add_package(CURL)
find_package(CURL CONFIG REQUIRED)

add_executable(foo foo.cpp)
target_link_libraries(foo PUBLIC CURL::libcurl)
