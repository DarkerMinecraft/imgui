# CMakeLists.txt for ImGui

cmake_minimum_required(VERSION 3.10)
project(ImGui)

# Use at least C++11 (required by ImGui)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# List the ImGui source files.
# (You can remove the demo file if you don't want to compile it.)
set(IMGUI_SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imgui_tables.cpp
)

# Create a static library target named "imgui"
add_library(ImGui STATIC ${IMGUI_SOURCES})

# Ensure that users of this library will include headers from this directory.
target_include_directories(ImGui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
