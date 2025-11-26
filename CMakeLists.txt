cmake_minimum_required(VERSION 3.6)
project(ModLoader)

# Use C++20 (NDK supports up to C++20; C++26 is not supported)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Collect all source and header files
file(GLOB_RECURSE sourceFiles CONFIGURE_DEPENDS "src/*.cpp" "src/*.hpp")

# Include project headers
include_directories(src)

# Build shared library (.so)
add_library(ModLoader SHARED ${sourceFiles})

# Optional: precompiled header (if you have headers.hpp)
# target_precompile_headers(ModLoader PRIVATE src/headers.hpp)

# Set position independent code (required for shared libraries on Android)
set_target_properties(ModLoader PROPERTIES POSITION_INDEPENDENT_CODE ON)

# Optional compiler flags for Android
if(CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    target_compile_options(ModLoader PRIVATE -Wall -O2)
endif()

# If your mod requires Android JNI, you can include NDK headers like this:
# include_directories(${ANDROID_NDK}/sysroot/usr/include)
# include_directories(${ANDROID_NDK}/sysroot/usr/include/android) 
