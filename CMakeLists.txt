cmake_minimum_required(VERSION 3.6)
project(ImGui LANGUAGES CXX)

add_library(ImGui STATIC)

set_target_properties(ImGui PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE}/ImGui"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE}/ImGui"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE}/ImGui"
)

target_sources(ImGui PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/imconfig.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui_internal.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/imstb_rectpack.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imstb_textedit.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imstb_truetype.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/imgui_tables.cpp"
)

set_target_properties(ImGui PROPERTIES CXX_STANDARD 17 CXX_STANDARD_REQUIRED ON)

if (WIN32)
    target_compile_definitions(ImGui PRIVATE "_CRT_SECURE_NO_WARNINGS")
    set_target_properties(ImGui PROPERTIES MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
elseif (UNIX AND NOT APPLE)
    set_target_properties(ImGui PROPERTIES POSITION_INDEPENDENT_CODE ON)
endif()

target_compile_options(ImGui PRIVATE
    $<$<CONFIG:Debug>:/Zi>           
    $<$<CONFIG:Release>:/O2>       
)
target_compile_definitions(ImGui PRIVATE
    $<$<CONFIG:Debug>:IMGUI_DEBUG>  
)