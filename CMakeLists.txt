cmake_minimum_required(VERSION 3.16)

# append
set(CMAKE_TOOLCHAIN_FILE "/home/pmy/CrossCompile/qt6/pi/lib/cmake/Qt6/qt.toolchain.cmake")

project(HelloVs VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.4 REQUIRED COMPONENTS Quick)

qt_standard_project_setup()

qt_add_executable(appHelloVs
    main.cpp
)

qt_add_qml_module(appHelloVs
    URI HelloVs
    VERSION 1.0
    QML_FILES Main.qml
)

set_target_properties(appHelloVs PROPERTIES
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appHelloVs
    PRIVATE Qt6::Quick
)

include(GNUInstallDirs)
install(TARGETS appHelloVs
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)