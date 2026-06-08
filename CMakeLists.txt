cmake_minimum_required(VERSION 3.15)
project(MyworldEngine)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

include(ExternalProject)
ExternalProject_Add(ogre_build
    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Contribs/ogre
    BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR}/ogre_build
    INSTALL_DIR ${CMAKE_CURRENT_BINARY_DIR}/ogre_install
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=${CMAKE_CURRENT_BINARY_DIR}/ogre_install
        -DCMAKE_BUILD_TYPE=Release
        -DOGRE_BUILD_SAMPLES=OFF
        -DOGRE_BUILD_TOOLS=OFF
        -DOGRE_BUILD_TESTS=OFF
    )

add_library(OgreMain SHARED IMPORTED GLOBAL)
set_target_properties(OgreMain PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_BINARY_DIR}/ogre_install/lib/libOgreMain.so
    INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_BINARY_DIR}/ogre_install/include/OGRE
    )

file(GLOB MYWORLD_SOURCES "src/*.cpp")
add_executable(Myworld ${MYWORLD_SOURCES})
target_link_libraries(Myworld PRIVATE OgreMain dl pthread)
add_dependencies(Myworld ogre_build)

set_target_properties(Myworld PROPERTIES
    BUILD_RPATH "${CMAKE_CURRENT_BINARY_DIR}/ogre_install/lib"
)
