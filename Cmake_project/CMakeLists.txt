cmake_minimum_required(VERSION 3.16)

project(Cprojecttemplate VERSION 1.0.0 LANGUAGES C)

# Include the header files
include_directories(include)

# Add the library
add_library(Library STATIC src/my_Clib.c)

# Add the executable
add_executable(Executable src/helloCworld.c)

# Link the library to the executable
target_link_libraries(Executable PUBLIC Library)

