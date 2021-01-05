cmake_minimum_required(VERSION 3.0)

project(imnodes)
set(version 0.1)

set(OpenGL_GL_PREFERENCE "GLVND")
find_package(OpenGL REQUIRED)

find_package(imgui QUIET COMPONENTS imgui-core)

option(BUILD_SHARED_LIBS "Build shared libs" ON)

add_subdirectory(imnodes-core)

option(BUILD_IMNODES_EXAMPLES "Build imnodes examples" ON)
if (${BUILD_IMNODES_EXAMPLES})
  add_subdirectory(examples)
endif()

configure_file(${PROJECT_NAME}-config.cmake
  "${CMAKE_BINARY_DIR}/${PROJECT_NAME}-config.cmake"
  @ONLY
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake"
  VERSION ${version}
  COMPATIBILITY AnyNewerVersion
)

install(
  FILES
    "${CMAKE_BINARY_DIR}/${PROJECT_NAME}-config.cmake"
  DESTINATION lib/cmake/${PROJECT_NAME}
)