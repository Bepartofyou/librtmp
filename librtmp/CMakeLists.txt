aux_source_directory(. SRC_LIST)
file(GLOB LIBRTMP_HEADERS ${CMAKE_SOURCE_DIR}/librtmp/*.h*)

add_definitions(
    -fPIC
    -Wall
    -DDEBUG
    -DNO_CRYPTO
    -D_CRT_SECURE_NO_WARNINGS
    -D_WINSOCK_DEPRECATED_NO_WARNINGS
)

add_library(rtmp STATIC ${LIBRTMP_HEADERS} ${SRC_LIST})

if(MICROSOFT)
    target_link_libraries(rtmp 
    ws2_32 winmm gdi32
    )
elseif(DARWIN)  
    #target_link_libraries(rtmp )
elseif(LINUX)
    #target_link_libraries(rtmp )
else()
    message(FATAL_ERROR "Unsupported system: ${CMAKE_SYSTEM_NAME}")
endif()
# install(TARGETS rtmp
#         RUNTIME DESTINATION ${CMAKE_SOURCE_DIR}/libs/bin
#         LIBRARY DESTINATION ${CMAKE_SOURCE_DIR}/libs/lib
#         ARCHIVE DESTINATION ${CMAKE_SOURCE_DIR}/libs/lib/static)
# install(FILES LIBRTMP_HEADERS DESTINATION  ${CMAKE_SOURCE_DIR}/libs/include)