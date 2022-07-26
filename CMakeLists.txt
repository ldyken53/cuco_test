cmake_minimum_required(VERSION 3.22)
set(CMAKE_CUDA_COMPILER /usr/local/cuda-11.7/bin/nvcc)
project(GPUJoin CUDA CXX)
set(CMAKE_CUDA_STANDARD 14)
set(CMAKE_CXX_STANDARD 14)
add_executable(GPUJoin static_map_example.cu)
set_target_properties(GPUJoin PROPERTIES CUDA_SEPARABLE_COMPILATION ON)

include(cmake/CPM.cmake)

CPMAddPackage(
  NAME cuco
  GITHUB_REPOSITORY NVIDIA/cuCollections
  GIT_TAG dev
  OPTIONS
     "BUILD_TESTS OFF"
     "BUILD_BENCHMARKS OFF"
     "BUILD_EXAMPLES OFF"
)

target_link_libraries(GPUJoin cuco)