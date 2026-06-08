cmake_minimum_required(VERSION 3.15)
project(MyworldGame)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OGRE REQUIRED COMPONENTS Bites CONFIG)

add_executable(MyworldGame src/main.cpp)  # or wherever your main.cpp is

target_link_libraries(MyworldGame OGRE::Bites)
