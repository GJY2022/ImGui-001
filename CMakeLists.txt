cmake_minimum_required(VERSION 3.27)

project(ImGui-001)

set(CMAKE_CXX_STANDARD 20)

include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/CPM.cmake)

CPMAddPackage(gh:ocornut/imgui@1.89)

file(GLOB SRC_LIB
    ${imgui_SOURCE_DIR}/*.cpp
    ${imgui_SOURCE_DIR}/examples/libs/gl3w/GL/gl3w.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp
)

include_directories(imgui INTERFACE
    ${imgui_SOURCE_DIR}/
    ${imgui_SOURCE_DIR}/backends/
    ${imgui_SOURCE_DIR}/examples/libs/gl3w/GL/
)

add_library(imgui STATIC ${SRC_LIB})

SET(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/lib)

link_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)

link_libraries(imgui)

target_link_libraries(imgui GL glfw)

file(GLOB SRC ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/build/bin)

add_executable(ikun ${SRC})


