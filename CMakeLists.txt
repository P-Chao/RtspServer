cmake_minimum_required(VERSION 3.5)
project(rtspserver)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSOCKLEN_T=socklen_t -g ")

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

find_package(OpenSSL REQUIRED)

# MPP
#set(MPP_PATH /home/orangepi/code/mpp-develop/inc)
#set(MPP_LIBS /home/orangepi/code/mpp-develop/mpp/librockchip_mpp.so)
#include_directories(${MPP_PATH})

# OSAL
#set(OSAL_PATH /home/orangepi/code/mpp-develop/osal/inc/ /home/orangepi/code/mpp-develop/utils)
#set(OSAL_LIBS /home/orangepi/code/mpp-develop/osal/libosal.a /home/orangepi/code/mpp-develop/utils/libutils.a)
#include_directories(${OSAL_PATH})

# RKNN lib
#set(RKNN_API_PATH ${CMAKE_SOURCE_DIR}/lib)
#set(RKNN_RT_LIB ${RKNN_API_PATH}/aarch64/librknnrt.so)
#include_directories(${RKNN_API_PATH}/include)
#include_directories(${CMAKE_SOURCE_DIR}/3rdparty)

# RGA
#set(RGA_PATH ${CMAKE_SOURCE_DIR}/3rdparty/rga/RK3588)
#set(RGA_LIB ${RGA_PATH}/lib/Linux/aarch64/librga.so)
#include_directories(${RGA_PATH}/include)


aux_source_directory(src/xop SOURCE1)
aux_source_directory(src/net SOURCE2)

include_directories(    
    src    
    src/xop
    src/net
    src/3rdpart
    )

add_executable(rtsp_cvmat
example/rtsp_cvmat.cpp
${SOURCE1}
${SOURCE2}
src/3rdpart/md5/md5.hpp
)
target_link_libraries(rtsp_cvmat ${OpenCV_LIBS} ${RKNN_RT_LIB} OpenSSL::SSL OpenSSL::Crypto pthread)
#avcodec swscale avformat avutil

# add_executable(rh264
# example/rtsp_h264_file.cpp
# ${SOURCE1}
# ${SOURCE2}
# src/3rdpart/md5/md5.hpp
# )
# target_link_libraries(rh264 ${MPP_LIBS} ${OSAL_LIBS}  ${OpenCV_LIBS} OpenSSL::SSL OpenSSL::Crypto )

#add_executable(sample
#example/sample.cpp
#${SOURCE1}
#${SOURCE2}
#src/3rdpart/md5/md5.hpp
#)
#target_link_libraries(sample ${MPP_LIBS} ${OSAL_LIBS}  ${OpenCV_LIBS}  ${RKNN_RT_LIB} ${RGA_LIB} OpenSSL::SSL OpenSSL::Crypto )
