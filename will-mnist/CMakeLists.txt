project(will-mnist)

set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_COMPILER $ENV{CXX})
# set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -pthread -fopenmp")

if(CCCC_CPU)
set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -pthread -DNO_CUDA -DNDEBUG")
set(LINK_LIBRARIES  openblas)
else()
set(CMAKE_CXX_FLAGS "-O3 -std=c++17 -pthread -DNDEBUG")
set(LINK_LIBRARIES will-cuda cudnn cudart cublas openblas)
endif()
aux_source_directory(./ SRC_LIST)

include_directories(/usr/local/include ../include ../src ../../common ../will)
link_directories(.)

add_library(will-mnist SHARED ${SRC_LIST})
target_link_libraries(will-mnist will)

