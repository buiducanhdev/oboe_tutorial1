cmake_minimum_required(VERSION 3.4.1)

find_package (oboe REQUIRED CONFIG)
# Pull in parselib
set (PARSELIB_DIR ../../../../parselib)
#message("PARSELIB_DIR = " + ${PARSELIB_DIR})

# Pull in iolib
set (IOLIB_DIR ../../../../iolib)
#message("IOLIB_DIR = " + ${IOLIB_DIR})

include(${PARSELIB_DIR}/src/main/cpp/CMakeLists.txt)
include(${IOLIB_DIR}/src/main/cpp/CMakeLists.txt)

# Include the WavLib headers and shared sample code
include_directories(
        ${PARSELIB_DIR}/src/main/cpp
        ${IOLIB_DIR}/src/main/cpp)
# App specific sources
set (APP_SOURCES
        DrumPlayerJNI.cpp
)


# Build our own native library
add_library (native-lib SHARED ${APP_SOURCES} )

# Find the Oboe package
find_library(log-lib log)

target_compile_options(native-lib PRIVATE -Wall -Werror "$<$<CONFIG:RELEASE>:-Ofast>")


# Specify the libraries which our native library is dependent on, including Oboe
target_link_libraries(native-lib
        log
        oboe::oboe
        -Wl,--whole-archive
        iolib
        parselib
        -Wl,--no-whole-archive
)