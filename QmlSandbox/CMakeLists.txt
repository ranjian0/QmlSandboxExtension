# Copyright © 2016-2023. Savenkov Igor
# SPDX-License-Identifier: GPL-3.0-or-later

cmake_minimum_required (VERSION 3.25.0)

project (QtWasmTemplate
         LANGUAGES CXX)

if (NOT DEFINED ENV{EMSDK})
    message (FATAL_ERROR "EMSDK environment variable is not defined. Please install emscripten SDK and set EMSDK environment variable.")
endif ()

find_package (Qt6 REQUIRED COMPONENTS Quick)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable (QtWasmTemplate
    main.cpp
    emscriptenlistener.h
    emscriptenlistener.cpp)

set_target_properties (QtWasmTemplate
    PROPERTIES
        AUTOMOC ON
        CXX_STANDARD 20
        CXX_STANDARD_REQUIRED ON)

qt_add_qml_module (QtWasmTemplate
    URI QtTemplateModule
    VERSION 1.0
    QML_FILES Main.qml)

target_link_libraries (QtWasmTemplate PRIVATE Qt6::Quick)
