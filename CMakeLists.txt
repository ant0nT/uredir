cmake_minimum_required(VERSION 3.20)

project(uredir LANGUAGES C)
set (LIBUEV_PATH "usr/lib/libuev" CACHE PATH "path to uev library")
set (CMAKE_INSTALL_RPATH "../lib" CACHE PATH "rpath to lib")

set(SOURCE_PATH "${CMAKE_SOURCE_DIR}/src" )
set(INCLUDE_PATH "${CMAKE_SOURCE_DIR}/src" )
# message(WARNING ${SOURCE_PATH})
# message(WARNING ${SOURCE_PATH})

file( GLOB_RECURSE HS "${INCLUDE_PATH}/*.h" )
file( GLOB_RECURSE CS "${SOURCE_PATH}/*.c" )
message(WARNING ${CS})
# set (HS )
# set(CMAKE_INSTALL_RPATH "../lib")
message(WARNING ${LIBUEV_PATH})
INCLUDE_DIRECTORIES(${LIBUEV_PATH}/include)
link_directories(${LIBUEV_PATH}/lib)
set (SOURCES ${HS} ${CS} ${LIBUEV_PATH}/include/uev.h)

add_executable(uredir ${SOURCES})
TARGET_LINK_LIBRARIES(uredir uev.so)
target_include_directories(uredir PRIVATE ${LIBUEV_PATH}/include)

set_property(TARGET uredir PROPERTY POSITION_INDEPENDENT_CODE 1)
# SET(CMAKE_BUILD_RPATH_USE_ORIGIN TRUE)

set_target_properties(uredir PROPERTIES OUTPUT_NAME uredir)
# set_target_properties(uredir PROPERTIES
#         BUILD_WITH_INSTALL_RPATH FALSE
#         LINK_FLAGS "-Wl,-rpath,../lib,--disable-new-dtags")
# set_target_properties(uredir PROPERTIES INSTALL_RPATH CMAKE_INSTALL_RPATH)
# install(FILES ../OpenNI-Linux-x64-2.3.0.66/Redist/libOpenNI2.so TYPE LIB)

install (TARGETS 
            uredir
        RUNTIME
            DESTINATION bin
        
            # DESTINATION lib/

)

install (FILES 
        ${LIBUEV_PATH}/lib/libuev.so TYPE LIB
    )
