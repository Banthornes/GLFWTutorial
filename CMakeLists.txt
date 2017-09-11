cmake_minimum_required (VERSION 2.6)
project (GLFWTutorial)
# The version number.
set (GLFWTutorial_VERSION_MAJOR 1)
set (GLFWTutorial_VERSION_MINOR 0)

# Configure a header file to pass some of the CMake settings
# to the source code.
configure_file (
	"${PROJECT_SOURCE_DIR}/GLFWTutorialConfig.h.in" 
	"${PROJECT_BINARY_DIR}/GLFWTutorialConfig.h"
)

set(GLFW_ROOT CACHE PATH "${GLFW_ROOT}")

file(MAKE_DIRECTORY "GLFW")
file(COPY "${GLFW_ROOT}" DESTINATION "${PROJECT_SOURCE_DIR}")

# Add the binary tree to the search path for include files
# so that we will find GLFWTutorialConfig.h.
include_directories ("${PROJECT_BINARY_DIR}")

# Add the directory of GLFW.
add_subdirectory("glfw")

# Add the executable.
add_executable(GLFWTutorial main.cpp)

# Link against GLFW target
target_link_libraries(GLFWTutorial glfw)

# Add OpenGL if required
find_package(OpenGL  REQUIRED)

include_directories(GLFWTutorial ${OPENGL_INCLUDE_DIR})
 target_link_libraries(GLFWTutorial ${OPENGL_gl_LIBRARY})
