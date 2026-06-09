cmake_minimum_required(VERSION 3.15)
project(Myworld)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# opengl in linuX
find_package(OpenGL REQUIRED)

# executabel file
add_executable(Myworld 
    src/main.cpp
    src/glad.c
)

target_include_directories(Myworld PRIVATE 
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    
)

#link lib yep
target_link_libraries(Myworld glfw)

# 26.04 sup 
if(UNIX AND NOT APPLE)
    target_link_libraries(Myworld ${CMAKE_DL_LIBS})
endif()
