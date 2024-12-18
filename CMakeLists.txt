# Copyright (C) 2022 The Qt Company Ltd.
# SPDX-License-Identifier: LicenseRef-Qt-Commercial OR BSD-3-Clause

cmake_minimum_required(VERSION 3.21.1)
project(CustomGeometry VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(QT_QML_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/qml)
set(QML_IMPORT_PATH ${QT_QML_OUTPUT_DIRECTORY}
    CACHE STRING "Import paths for Qt Creator's code model"
    FORCE
)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Quick)
qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(${CMAKE_PROJECT_NAME}
    main.cpp
)

qt_add_qml_module(${CMAKE_PROJECT_NAME}
    URI CustomGeometry
    VERSION 1.0
    QML_FILES
        Main.qml
    SOURCES
        beziercurve.cpp
        beziercurve.h
)

target_link_libraries(${CMAKE_PROJECT_NAME}
    PRIVATE
        Qt6::Core
        Qt6::Gui
        Qt6::Quick
)


include(GNUInstallDirs)
install(TARGETS ${CMAKE_PROJECT_NAME}
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
