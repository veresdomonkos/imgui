cmake_minimum_required(VERSION 3.10)
project(imgui)

# The platform and renderer backends are off by default: an application with its own renderer and input layer needs
# only the core, and then nothing pulls in GLFW or Vulkan.
option(IMGUI_BACKENDS "Build the GLFW, OpenGL 3 and Vulkan backends" OFF)

set(IMGUI_SOURCES
    src/imgui.cpp
    src/imgui_demo.cpp
    src/imgui_draw.cpp
    src/imgui_tables.cpp
    src/imgui_widgets.cpp
)

add_library(imgui STATIC ${IMGUI_SOURCES})

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include/imgui
)

if (IMGUI_BACKENDS)
    find_package(Vulkan REQUIRED)
    target_sources(imgui PRIVATE
        src/backends/imgui_impl_glfw.cpp
        src/backends/imgui_impl_opengl3.cpp
        src/backends/imgui_impl_vulkan.cpp
    )
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include/imgui/backends)
    target_link_libraries(imgui PRIVATE Vulkan::Vulkan)
    target_link_libraries(imgui PUBLIC glfw)
endif()
