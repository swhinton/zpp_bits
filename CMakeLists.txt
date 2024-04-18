cmake_minimum_required(VERSION 3.22)
set(CMAKE_CXX_STANDARD 20)

project(zpp_bits
	VERSION 4.4.20
        HOMEPAGE_URL "https://github.com/eyalz800/zpp_bits"
        LANGUAGES CXX C)

include(GNUInstallDirs)
include(GenerateExportHeader)
include(CMakePackageConfigHelpers)


list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

add_library(${PROJECT_NAME} INTERFACE)
add_library(zpp_bits::${PROJECT_NAME} ALIAS ${PROJECT_NAME})
target_include_directories(${PROJECT_NAME}
    INTERFACE
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

include(CMakePackageConfigHelpers)
export(
        TARGETS ${PROJECT_NAME}
        NAMESPACE zpp_bits::
        FILE zpp_bitsTargets.cmake
)
configure_package_config_file(
    "${PROJECT_SOURCE_DIR}/cmake/Config.cmake.in"
    "zpp_bitsConfig.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/zpp_bits
    PATH_VARS
        CMAKE_INSTALL_LIBDIR
)

write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/zpp_bitsConfigVersion.cmake
    VERSION ${CMAKE_PROJECT_VERSION}
        COMPATIBILITY SameMinorVersion
)

install(
    FILES "${CMAKE_CURRENT_BINARY_DIR}/zpp_bitsConfig.cmake"
          "${CMAKE_CURRENT_BINARY_DIR}/zpp_bitsConfigVersion.cmake"
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/zpp_bits"
)

install(
    FILES ${PROJECT_SOURCE_DIR}/zpp_bits.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

