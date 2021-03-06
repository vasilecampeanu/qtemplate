cmake_minimum_required(VERSION 3.8)
set(This QTemplate)

# Set project name.
project(${This} VERSION 0.0.1 LANGUAGES C CXX)

set(CMAKE_AUTOUIC OFF)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

# Set the standard.
set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 99)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_C_STANDARD 17)
set(CMAKE_CXX_STANDARD 17)

set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find QT Creator Components
find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets LinguistTools REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets LinguistTools REQUIRED)

# This variable is used to initialize the POSITION_INDEPENDENT_CODE property on all the targets.
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Enables testing for this directory and below. 
enable_testing()

# Store a property of directory scope in the named variable.
get_directory_property(ParentDirectory PARENT_DIRECTORY)
if(ParentDirectory STREQUAL "")

    if(MSVC)
        option(RUNTIME_STATIC_LINKAGE "Link with runtime library statically" OFF)
    endif(MSVC)

    if(MSVC AND RUNTIME_STATIC_LINKAGE)
        foreach(flag
            CMAKE_C_FLAGS
            CMAKE_CXX_FLAGS
            CMAKE_C_FLAGS_DEBUG
            CMAKE_CXX_FLAGS_DEBUG
            CMAKE_C_FLAGS_RELEASE
            CMAKE_CXX_FLAGS_RELEASE
            CMAKE_C_FLAGS_MINSIZEREL
            CMAKE_CXX_FLAGS_MINSIZEREL
            CMAKE_C_FLAGS_RELWITHDEBINFO
            CMAKE_CXX_FLAGS_RELWITHDEBINFO
        )
            if(${flag} MATCHES "/MD")
                string(REGEX REPLACE "/MD" "/MT" ${flag} "${${flag}}")
            endif(${flag} MATCHES "/MD")
        endforeach(flag)
    endif(MSVC AND RUNTIME_STATIC_LINKAGE)

    # Keep Google Test's linkage of the runtime in sync with our own.
    if(MSVC)
        if(RUNTIME_STATIC_LINKAGE)
            set(gtest_force_shared_crt OFF CACHE BOOL "Use shared (DLL) run-time lib even when Google Test is built as static lib." FORCE)
        else(RUNTIME_STATIC_LINKAGE)
            set(gtest_force_shared_crt ON  CACHE BOOL "Use shared (DLL) run-time lib even when Google Test is built as static lib." FORCE)
        endif(RUNTIME_STATIC_LINKAGE)
    endif(MSVC)

    # Organize applications, libraries, etc. in folders in the IDE.
    set_property(GLOBAL PROPERTY USE_FOLDERS ON)

    # Ensure proper loading of side-loaded shared libraries on all targets.
    set(CMAKE_SKIP_BUILD_RPATH FALSE)
    set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
    if(APPLE)
        set(CMAKE_INSTALL_RPATH "@loader_path")
    elseif(UNIX)
        set(CMAKE_INSTALL_RPATH "\$ORIGIN")
    endif()

    # Don't add "d" postfix for debug builds of libraries.
    set(CMAKE_DEBUG_POSTFIX "")

    # Suppress Microsoft warnings about functions being unsafe.
    add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_SCL_SECURE_NO_WARNINGS)    

    # External libraries

endif(ParentDirectory STREQUAL "")

# Add subdirectories directly in this repository.
add_subdirectory(template)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})