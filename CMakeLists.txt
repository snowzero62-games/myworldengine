cmake_minimum_required(VERSION 3.15)
project(MyworldGame)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OGRE REQUIRED COMPONENTS Bites CONFIG)
include_directories(${CMAKE_SOURCE_DIR}/include)
add_executable(MyworldGame src/*.cpp)

target_link_libraries(MyworldGame OGRE::Bites)
