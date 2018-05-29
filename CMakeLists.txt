cmake_minimum_required(VERSION 2.8)
project(rtmp C CXX)

set (CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(haiUtil)
include(FindPkgConfig)
include(FindThreads)

# Platform shortcuts
set_if(DARWIN      ${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
set_if(LINUX       ${CMAKE_SYSTEM_NAME} MATCHES "Linux")
set_if(MICROSOFT   WIN32 AND (NOT MINGW AND NOT CYGWIN))
set_if(SYMLINKABLE LINUX OR DARWIN OR CYGWIN)

add_subdirectory(librtmp)
set(RTMPDUMP_SRC rtmpdump.c getopt.c getopt.h)
set(RTMPSRV_SRC rtmpsrv.c thread.c thread.h getopt.c getopt.h)
set(RTMPSUCK_SRC rtmpsuck.c thread.c thread.h getopt.c getopt.h)
set(RTMPGW_SRC rtmpgw.c thread.c thread.h getopt.c getopt.h)

add_definitions(
    -fPIC
    -Wall
    -DDEBUG
    -DNO_CRYPTO
    -D_CRT_SECURE_NO_WARNINGS
    -D_WINSOCK_DEPRECATED_NO_WARNINGS
    -DRTMPDUMP_VERSION="2.4"
)

include_directories(${CMAKE_SOURCE_DIR}/librtmp)
if(MICROSOFT)
    link_directories(${CMAKE_SOURCE_DIR}/build/librtmp/Debug)
else()
    link_directories(${CMAKE_SOURCE_DIR}/build/librtmp/)
endif()

add_executable(rtmpdump ${RTMPDUMP_SRC})
add_executable(rtmpsrv  ${RTMPSRV_SRC})
add_executable(rtmpsuck ${RTMPSUCK_SRC})
add_executable(rtmpgw   ${RTMPGW_SRC})

if(MICROSOFT)
    target_link_libraries(rtmpdump 
    ws2_32 winmm gdi32 rtmp
    )
    target_link_libraries(rtmpsrv 
    ws2_32 winmm gdi32 rtmp
    )
    target_link_libraries(rtmpsuck 
    ws2_32 winmm gdi32 rtmp
    )
    target_link_libraries(rtmpgw 
    ws2_32 winmm gdi32 rtmp
    )
elseif(DARWIN)  
    target_link_libraries(rtmpdump 
    rtmp
    )
    target_link_libraries(rtmpsrv 
    rtmp
    )
    target_link_libraries(rtmpsuck 
    rtmp
    )
    target_link_libraries(rtmpgw 
    rtmp
    )
elseif(LINUX)
    target_link_libraries(rtmpdump 
    rtmp
    )
    target_link_libraries(rtmpsrv 
    rtmp
    )
    target_link_libraries(rtmpsuck 
    rtmp
    )
    target_link_libraries(rtmpgw 
    rtmp
    )
else()
    message(FATAL_ERROR "Unsupported system: ${CMAKE_SYSTEM_NAME}")
endif()