cmake_minimum_required(VERSION 3.10)
project(imgui)

set(IMGUI_SOURCES
    src/imgui.cpp
    src/imgui_demo.cpp
    src/imgui_draw.cpp
    src/imgui_tables.cpp
    src/imgui_widgets.cpp
)

set(BACKEND_SOURCES
    src/backends/imgui_impl_glfw.cpp
    src/backends/imgui_impl_opengl3.cpp
)

add_library(imgui STATIC ${IMGUI_SOURCES} ${BACKEND_SOURCES})

target_include_directories(imgui PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/include/imgui/backends
)

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(imgui PUBLIC glfw)
