cmake_minimum_required(VERSION 2.8)
project(rtmp C CXX)

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
link_directories(${CMAKE_SOURCE_DIR}/build/librtmp/Debug)

add_executable(rtmpdump ${RTMPDUMP_SRC})
add_executable(rtmpsrv  ${RTMPSRV_SRC})
add_executable(rtmpsuck ${RTMPSUCK_SRC})
add_executable(rtmpgw   ${RTMPGW_SRC})

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