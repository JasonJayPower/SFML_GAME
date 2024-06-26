#Require a minimum version of cmake.
cmake_minimum_required(VERSION 3.15)

#Set the name of the project.
project(SFML_GAME
    VERSION 1.0
    DESCRIPTION "SFML GAME"
    LANGUAGES CXX)

# Global flag to cause add_library() to create shared libraries if on.
set(BUILD_SHARED_LIBS FALSE)

#Adds a subdirectory to the build.
add_subdirectory(libs/sfml)

# File manipulation command. (Automatically checks and finds all source files at build time)
file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS "src/*.cpp")

# Add an executable to the project using the specified source files.
add_executable(${PROJECT_NAME} ${SRC_FILES})

# Add expected compiler features to a target.
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)

# Add compile options to a target. Recommend appending /WX to treat all warnings as errors.
target_compile_options(${PROJECT_NAME} PRIVATE $<$<CXX_COMPILER_ID:MSVC>:/W4>)

# Add include directories to a target.
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_SOURCE_DIR}/src)

# Specify libraries or flags to use when linking a given target.
target_link_libraries(${PROJECT_NAME} PRIVATE sfml-system sfml-audio sfml-graphics sfml-network sfml-window)

