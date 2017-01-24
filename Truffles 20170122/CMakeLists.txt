#see: https://cmake.org/Wiki/CMake_Cross_Compiling
# https://cmake.org/Wiki/CMake_RPATH_handling

cmake_minimum_required(VERSION 3.6)
project(Truffles_20170122)

set(ARM_PREFIX /usr/local/bin/arm-frc-linux-gnueabi)
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_C_COMPILER ${ARM_PREFIX}-gcc)
set(CMAKE_CXX_COMPILER ${ARM_PREFIX}-g++)


#set(CMAKE_CXX_FLAGS "-std=c++1y -Wformat=2 -Wall -Wextra -Werror -pedantic -Wno-psabi" CACHE STRING "" FORCE)
#set(CMAKE_CXX_FLAGS_DEBUG "-O0 -g3" CACHE STRING "" FORCE)
#set(CMAKE_CXX_FLAGS_RELEASE "-O3 -g" CACHE STRING "" FORCE) # still want debugging for release?





set(CMAKE_CXX_STANDARD 14)

set(WPI_DIR "$ENV{HOME}/wpilib")


include_directories(SYSTEM
        "${WPI_DIR}/cpp/current/include"
        "${WPI_DIR}/user/cpp/include")
link_directories(SYSTEM
        "${WPI_DIR}/cpp/current/lib"
        "${WPI_DIR}/user/cpp/lib")
#gcc: -O0 -g3 -Wall -c -fmessage-length=0
#g++: -std=c++1y -I"/Users/jason/wpilib/cpp/current/include" -I"/Users/jason/Documents/workspace/Truffles/src" -O0 -g3 -Wall -c -fmessage-length=0
#linker: -L"/Users/jason/wpilib/cpp/current/lib" -Wl,-rpath,/opt/GenICam_v2_3/bin/Linux_armv7-a,-rpath,/usr/local/frc/rpath-lib


set(CMAKE_INSTALL_RPATH "/opt/GenICam_v2_3/bin/Linux_armv7-a")



file(GLOB_RECURSE SOURCE_FILES src/*.cpp)



add_executable(Truffles ${SOURCE_FILES})
target_link_libraries(Truffles wpi)