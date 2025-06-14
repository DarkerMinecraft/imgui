cmake_minimum_required(VERSION 3.16)
project(ImGui)

# Create static library
add_library(ImGui STATIC)

# Set C++ standard
set_property(TARGET ImGui PROPERTY CXX_STANDARD 17)

# Find source files (only the ones you need for your project)
set(IMGUI_SOURCES
    imconfig.h
    imgui.cpp
    imgui.h
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_internal.h
    imgui_tables.cpp
    imgui_widgets.cpp
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    backends/imgui_impl_win32.cpp
)

# Add source files to the target
target_sources(ImGui PRIVATE ${IMGUI_SOURCES})

# Include directories
target_include_directories(ImGui 
    PUBLIC 
        ${CMAKE_CURRENT_SOURCE_DIR}
)
# Set output directories to match the project structure
set_target_properties(ImGui PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/$<CONFIG>
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/$<CONFIG>
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/$<CONFIG>
)

# Disable warnings from ImGui code
if(MSVC)
    target_compile_options(ImGui PRIVATE /W3 /wd4996 /wd4530)
else()
    target_compile_options(ImGui PRIVATE -Wall -Wno-unused-variable -Wno-unused-function)
endif()
