# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

add_library(opentelemetry_version version.cc)

set_target_properties(opentelemetry_version PROPERTIES EXPORT_NAME version)
set_target_version(opentelemetry_version)

target_link_libraries(opentelemetry_version PUBLIC opentelemetry_api
                                                   opentelemetry_sdk)

target_include_directories(
  opentelemetry_version
  PUBLIC "$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/sdk/include>")

if(OPENTELEMETRY_INSTALL)
  install(
    TARGETS opentelemetry_version
    EXPORT "${PROJECT_NAME}-sdk-target"
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT sdk)

  opentelemetry_add_pkgconfig(
    version "OpenTelemetry SDK - Version"
    "A library exporting version information for OpenTelemetry."
    "opentelemetry_api")
endif()
