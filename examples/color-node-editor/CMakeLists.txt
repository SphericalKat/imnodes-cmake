cmake_minimum_required(VERSION 2.8.12)

project(color-node-editor)

set(OpenGL_GL_PREFERENCE "GLVND")
find_package(OpenGL REQUIRED)

find_package(SDL2 REQUIRED CONFIG)
find_package(imgui QUIET COMPONENTS gl3w imgui-core imgui-sdl imgui-opengl3)
find_package(imnodes QUIET COMPONENTS imnodes-core)

set(srcs 
    ${CMAKE_SOURCE_DIR}/imnodes/example/color_node_editor.cpp
    ${CMAKE_SOURCE_DIR}/imnodes/example/main.cpp)
add_executable(${PROJECT_NAME} ${srcs})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${OPENGL_INCLUDE_DIR}
    ${SDL2_INCLUDE_DIRS}
    gl3w
    imgui-core
    imgui-sdl
    imgui-opengl3
    imnodes-core)

target_link_libraries(${PROJECT_NAME}
        ${CMAKE_DL_LIBS}
        ${SDL2_LIBRARIES}
        gl3w
        imgui-core
        imgui-sdl
        imgui-opengl3
        imnodes-core)

install(TARGETS ${PROJECT_NAME} DESTINATION bin)