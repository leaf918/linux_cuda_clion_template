cmake_minimum_required(VERSION 3.6)
PROJECT(lbmslv)

FIND_PACKAGE(CUDA REQUIRED)

INCLUDE(FindCUDA)

#INCLUDE_DIRECTORIES(/usr/local/cuda/include ${MPI_INCLUDE_PATH})

FILE(GLOB SOURCES "*.cu" "*.cpp" "*.c" "*.h")
CUDA_ADD_EXECUTABLE(lbmslv ${SOURCES})

LIST(APPEND CMAKE_CXX_FLAGS "-std=c++0x -O3 -ffast-math -Wall")

LIST(APPEND CUDA_NVCC_FLAGS --compiler-options -fno-strict-aliasing -lineinfo -use_fast_math -Xptxas -dlcm=cg)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_20,code=sm_20)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_30,code=sm_30)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_35,code=sm_35)

TARGET_LINK_LIBRARIES(lbmslv /usr/local/cuda/lib64/libcudart.so)
