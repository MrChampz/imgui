cmake_minimum_required(VERSION 3.20)
project("imgui")

# Files
add_library(${PROJECT_NAME} STATIC
    ${CMAKE_CURRENT_LIST_DIR}/imconfig.h
    ${CMAKE_CURRENT_LIST_DIR}/imgui.h
    ${CMAKE_CURRENT_LIST_DIR}/imgui.cpp
    ${CMAKE_CURRENT_LIST_DIR}/imgui_draw.cpp
    ${CMAKE_CURRENT_LIST_DIR}/imgui_internal.h
    ${CMAKE_CURRENT_LIST_DIR}/imgui_tables.cpp
    ${CMAKE_CURRENT_LIST_DIR}/imgui_widgets.cpp
    ${CMAKE_CURRENT_LIST_DIR}/imstb_rectpack.h
    ${CMAKE_CURRENT_LIST_DIR}/imstb_textedit.h
    ${CMAKE_CURRENT_LIST_DIR}/imstb_truetype.h
    ${CMAKE_CURRENT_LIST_DIR}/imgui_demo.cpp
)

# Set output name
set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}")

# Properties

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED)

set_target_properties(${PROJECT_NAME} PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${OUTPUT_DIR}/Vendor/${PROJECT_NAME}"
    LIBRARY_OUTPUT_DIRECTORY "${OUTPUT_DIR}/Vendor/${PROJECT_NAME}"
    RUNTIME_OUTPUT_DIRECTORY "${OUTPUT_DIR}/Vendor/${PROJECT_NAME}"
)

# Compile definitions

if (WIN32)
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "IMGUI_API=__declspec(dllexport)"
    )
endif()

# Include dirs

target_include_directories(${PROJECT_NAME} PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
    $<INSTALL_INTERFACE:imgui.h>
    $<INSTALL_INTERFACE:imconfig.h>
)
