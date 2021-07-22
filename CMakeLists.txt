cmake_minimum_required(VERSION 3.14...3.21)

# libdes-l-4.01a from
# https://agentpp.com/download/libdes-l-4.01a.tar.gz
#
project(
  des
  VERSION 4.1.1.1
  LANGUAGES C
)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

add_library(
  des STATIC
  des.h
  cbc_enc.c
  ncbc_enc.c
  ecb_enc.c
  ede_enc.c
  fcrypt.c
  set_key.c
  des_enc.c
)
target_compile_definitions(des PRIVATE LIBDES_LIT)
target_include_directories(des PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SORUCE_DIR}> $<INSTALL_INTERFACE:include>)


# TODO add_subdirectory(examples)

# NOTE: we use packageProject! CK
# XXX install(TARGETS des LIBRARY)
# XXX install(FILES des.h TYPE INCLUDE)

include(PackageProject)
# XXX CPMAddPackage("gh:TheLartians/PackageProject.cmake@1.8.0")

packageProject(
  # the name of the target to export
  NAME ${PROJECT_NAME}
  # the version of the target to export
  VERSION ${PROJECT_VERSION}
  # a temporary directory to create the config files
  BINARY_DIR ${PROJECT_BINARY_DIR}
  # location of the target's public headers
  INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include
  # should match the target's INSTALL_INTERFACE include directory
  INCLUDE_DESTINATION include
  # semicolon separated list of the project's dependencies
  DEPENDENCIES ""
  # (optional) create a header containing the version info
  # Note: that the path to headers should be lowercase
  ## VERSION_HEADER "${PROJECT_NAME}/version.h"
  # (optional) create a export header using GenerateExportHeader module
  ## EXPORT_HEADER "${PROJECT_NAME}/export.h"
  # (optional) install your library with a namespace (Note: do NOT add extra '::')
  NAMESPACE ${PROJECT_NAME}
  # (optional) define the project's version compatibility, defaults to `AnyNewerVersion`
  # supported values: `AnyNewerVersion|SameMajorVersion|SameMinorVersion|ExactVersion`
  COMPATIBILITY SameMajorVersion
  # (optional) option to disable the versioning of install destinations
  DISABLE_VERSION_SUFFIX YES
  # (optional) option to ignore target architecture for package resolution
  # defaults to YES for header only (i.e. INTERFACE) libraries
  ## ARCH_INDEPENDENT YES
)

