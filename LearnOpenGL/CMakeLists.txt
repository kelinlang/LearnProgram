﻿# CMakeList.txt: LearnProgramC 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
#cmake_minimum_required (VERSION 3.8)

include_directories("D:/work/OpenGL/glew-2.1.0/include")
#link_directories("D:/work/OpenGL/glew-2.1.0/lib/Release/Win32")
link_directories("D:/work/OpenGL/glew-2.1.0/lib/Release/x64")

#include_directories("D:/work/OpenGL/glfw-3.3.2.bin.WIN32/include")
#link_directories("D:/work/OpenGL/glfw-3.3.2.bin.WIN32/lib-vc2019")
include_directories("D:/work/OpenGL/glfw-3.3.2.bin.WIN64/include")
link_directories("D:/work/OpenGL/glfw-3.3.2.bin.WIN64/lib-vc2019")

#list(APPEND LINK_LIB_LIST  glew32.lib   glew32s.lib glfw3.lib glfw3dll.lib)
list(APPEND LINK_LIB_LIST opengl32.lib  glew32s.lib glew32.lib    glfw3.lib glfw3dll.lib)

#glm lib
set(glm ${CMAKE_CURRENT_SOURCE_DIR}/glm)
#add_subdirectory (${glm}/glm)
#file(GLOB glm_src_list ${glm}/*/*.hpp ${glm}/*/*/*.hpp  ${glm}/*/*/*.inl  ${glm}/*/*/*.* ${glm}/*.hpp   ${glm}/*.hpp      ${glm}/*/*.h ${glm}/*.h )
#file(GLOB glm_src_list ${glm}/*/*.hpp ${glm}/*/*/*.hpp  )
#add_library(glm STATIC ${glm_src_list})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/glm)

#soil lib
set(soil ${CMAKE_CURRENT_SOURCE_DIR}/soil)
file(GLOB soil_src_list ${soil}/*/*.c ${soil}/*.c ${soil}/*/*.h ${soil}/*.h )
add_library(soil STATIC ${soil_src_list})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/soil)

set(CommonLibRoot ${CMAKE_CURRENT_SOURCE_DIR}/cpp)

file(GLOB CommonLib_src_list ${CommonLibRoot}/*/*.cpp ${CommonLibRoot}/*.cpp ${CommonLibRoot}/*/*.h ${CommonLibRoot}/*.h )

# 将源代码添加到此项目的可执行文件。
add_executable (TestOpenGL "TestOpenGL.cpp"  ${CommonLib_src_list})
target_link_libraries(TestOpenGL  ${LINK_LIB_LIST}  ${CMAKE_THREAD_LIBS_INIT})

add_executable (TestOpenGLCamera "TestCamera.cpp" "shader.h" "Camera.h"   ${CommonLib_src_list})
target_link_libraries(TestOpenGLCamera  ${LINK_LIB_LIST}  ${CMAKE_THREAD_LIBS_INIT} soil )
# TODO: 如有需要，请添加测试并安装目标。
