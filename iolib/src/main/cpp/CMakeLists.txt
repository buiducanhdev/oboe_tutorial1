# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.
cmake_minimum_required(VERSION 3.4.1)
set(PARSELIB_DIR ../../../../parselib)
find_package(oboe REQUIRED CONFIG)

# include folders
include_directories(
        ${PARSELIB_DIR}/src/main/cpp
        ${CMAKE_CURRENT_LIST_DIR}
        ../../../../shared)


add_library( # Sets the name of the library.
        iolib

        # Sets the library as a static library.
        STATIC

        # source
        ${CMAKE_CURRENT_LIST_DIR}/player/SampleSource.cpp
        ${CMAKE_CURRENT_LIST_DIR}/player/SampleBuffer.cpp
        ${CMAKE_CURRENT_LIST_DIR}/player/OneShotSampleSource.cpp
        ${CMAKE_CURRENT_LIST_DIR}/player/SimpleMultiPlayer.cpp)

target_link_libraries( # Specifies the target library.
        iolib

        # Links the target library to the log library
        # included in the NDK.
        oboe::oboe
        log)
