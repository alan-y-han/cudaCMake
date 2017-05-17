cmake_minimum_required(VERSION 3.0)
project(printCubes)

find_package(CUDA REQUIRED)

# Pass options to NVCC
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS}
    -O3 -Xcompiler -Wextra)

# Find all source files
file(GLOB_RECURSE SRC "src/*.cpp")
file(GLOB_RECURSE CUDASRC "src/*.cu")
file(GLOB_RECURSE HDR "include/*.h")
list(APPEND SRC ${HDR})
list(APPEND SRC ${CUDASRC})

# Specify binary name and source file to build it from
cuda_add_library(${PROJECT_NAME} ${SRC})

target_include_directories(${PROJECT_NAME} PUBLIC "include")

export(PACKAGE ${PROJECT_NAME})
export(TARGETS ${PROJECT_NAME}
  FILE "${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake")


# ### CMakeLists.txt for CUDA

# cmake_minimum_required(VERSION 2.8)
# find_package(CUDA QUIET REQUIRED)

# # Pass options to NVCC
# set(
#     CUDA_NVCC_FLAGS
#     ${CUDA_NVCC_FLAGS};
#     -O3 -gencode arch=compute_22,code=sm_22
#     )

# # Specify include directories
# include_directories(
#     kernels
#     utility
#     )

# # Specify library paths
# link_directories(
#     /opt/foobar/lib
#     /opt/joestuff/lib
#     )

# # For compilation ...
# # Specify target & source files to compile it from
# cuda_add_executable(
#     hellocuda
#     hellocuda.cu
#     hellocuda.h
#     kernels/hellokernels.cu
#     kernels/hellokernels.h
#     utility/wrapper.cpp
#     utility/wrapper.h
#     )

# # For linking ...
# # Specify target & libraries to link it with
# target_link_libraries(
#     hellocuda
#     -lfoobar
#     -ljoestuff
#     )