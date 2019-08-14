# CMake entry point
cmake_minimum_required (VERSION 2.6)
project (IKCreator)

find_package(OpenGL REQUIRED)

add_subdirectory (external)

if(INCLUDE_DISTRIB)
    add_subdirectory(distrib)
endif(INCLUDE_DISTRIB)

include_directories(
#    external/AntTweakBar-1.16/include/
    external/glfw-3.3/include/GLFW/
    external/glm-0.9.9.5/
    external/glew-2.1.0/include/
#    external/assimp-3.0.1270/include/
#    external/bullet-2.81-rev2613/src/
    .
    )

set(ALL_LIBS
    ${OPENGL_LIBRARY}
    glfw
    GLEW_210
    )

add_definitions(
    -DTW_STATIC
    -DTW_NO_LIB_PRAGMA
    -DTW_NO_DIRECT3D
    -DGLEW_STATIC
    -D_CRT_SECURE_NO_WARNINGS
    )

# IKCreator
add_executable(IKCreator
    IKCreator/main.cpp
    )
target_link_libraries(IKCreator
    ${ALL_LIBS}
    )
# Xcode and Visual working directories
set_target_properties(IKCreator PROPERTIES XCODE_ATTRIBUTE_CONFIGURATION_BUILD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/IKCreator/")
