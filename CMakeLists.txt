cmake_minimum_required(VERSION 3.10)
project(ImGui_SDL2_OpenGL3)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add source files
set(IMGUI_DIR ${CMAKE_SOURCE_DIR}/imgui)
set(IMGUI_BACKEND_DIR ${IMGUI_DIR}/backends)

set(SOURCE_FILES
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/imgui_impl_sdl2.cpp
    ${IMGUI_DIR}/imgui_impl_opengl3.cpp


    #${IMGUI_BACKEND_DIR}/imgui_impl_sdl2.cpp
    #${IMGUI_BACKEND_DIR}/imgui_impl_opengl3.cpp
    src/Main.cpp
)

# Add executable
add_executable(${PROJECT_NAME} ${SOURCE_FILES})

# Find SDL2 and OpenGL
find_package(SDL2 REQUIRED)
find_package(OpenGL REQUIRED)

# Find GLEW manually
find_path(GLEW_INCLUDE_DIR NAMES GL/glew.h)
find_library(GLEW_LIBRARY NAMES GLEW glew32 glew glew32s PATH_SUFFIXES lib)

# Include directories
include_directories(${SDL2_INCLUDE_DIRS} ${OPENGL_INCLUDE_DIR} ${GLEW_INCLUDE_DIR} ${IMGUI_DIR} ${IMGUI_BACKEND_DIR})

# Link libraries
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} ${OPENGL_LIBRARIES} ${GLEW_LIBRARY})
