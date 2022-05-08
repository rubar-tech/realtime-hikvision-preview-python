cmake_minimum_required(VERSION 2.8.11)
project(npp_cuda)

#find_package(CUDA REQUIRED)
enable_language(CUDA)

set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS} --compiler-options -fPIC)

file(GLOB_RECURSE NPP_CUDA_HEADS *.h *.hpp *.cuh)
file(GLOB NPP_CUDA_SOURCES *.cpp *.cu)

source_group("Include" FILES ${NPP_CUDA_HEADS})
source_group("Source" FILES ${NPP_CUDA_SOURCES})

add_library(npp_cuda STATIC ${NPP_CUDA_HEADS} ${NPP_CUDA_SOURCES})
# comment this line for some versions of cuda exp 11.1
# target_link_libraries(npp_cuda ${CUDA_npp_LIBRARY})

# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libcudart.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppc.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppial.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppicc.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppidei.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppif.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppig.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppim.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppist.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppisu.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnppitc.so)
# target_link_libraries(npp_cuda /usr/local/cuda/lib64/libnpps.so)
