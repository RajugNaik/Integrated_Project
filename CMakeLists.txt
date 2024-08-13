cmake_minimum_required(VERSION 3.16)
project(IntegratedProject LANGUAGES C)

# Add subdirectory for the existing CMake-based project
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/Cmake_project")
    add_subdirectory(Cmake_project)
else()
    message(FATAL_ERROR "Cmake_project directory not found")
endif()

# Add custom target to build the Makefile-based project
add_custom_target(
    BuildMakefileProject ALL
    COMMAND make
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/project
    COMMENT "Building Makefile-based project"
)

# Include directories for both projects
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/project/include
    ${CMAKE_CURRENT_SOURCE_DIR}/Cmake_project/include
)

# Collect all source files from the CMake-based project
file(GLOB CMAKE_PROJECT_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/Cmake_project/src/*.c
)

# Define the executable for the integrated project
add_executable(IntegratedExecutable
    ${CMAKE_PROJECT_SOURCES}
)

# Link the CMake-based project's library
target_link_libraries(IntegratedExecutable PRIVATE Library)

# Copy the Makefile-based project executable to the build directory
add_custom_command(
    TARGET IntegratedExecutable
    PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
            ${CMAKE_CURRENT_SOURCE_DIR}/project/build/helloworld
            $<TARGET_FILE_DIR:IntegratedExecutable>/helloworld
    COMMENT "Copying Makefile-based project executable"
)

# Ensure the Makefile-based project is built before the final executable
add_dependencies(IntegratedExecutable BuildMakefileProject)

