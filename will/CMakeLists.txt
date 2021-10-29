project(will)
cmake_minimum_required(VERSION 2.6)

file(GLOB SRC_LIST 
    ./*.cpp
    ./layer/*.cpp
    ./*.c
    ../../common/*.cpp
    ../../common/*.c)

set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_COMPILER $ENV{CXX})

if(CCCC_CPU)
set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -pthread -DNO_CUDA -DNDEBUG")
set(LINK_LIBRARIES  openblas)
else()
set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -pthread -DNDEBUG")
set(LINK_LIBRARIES will-cuda cudnn cudart cublas openblas)
endif()
include_directories(../../common ../include . ./layer)
# link_directories(/usr/local/cuda/lib64)

add_library(will SHARED ${SRC_LIST})
target_link_libraries(will LINK_PRIVATE ${LINK_LIBRARIES})

install(TARGETS will LIBRARY DESTINATION lib)
