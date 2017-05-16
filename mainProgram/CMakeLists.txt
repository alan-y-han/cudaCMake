cmake_minimum_required(VERSION 3.0)

project(cudaCmakeLinkingTesting)

function(cond_find_package TARGET_NAME)
  if (NOT TARGET ${TARGET_NAME})
   find_package(${TARGET_NAME} ${ARGN})
  endif()
endfunction()

cond_find_package(printCubes REQUIRED)

# Find all source files
file(GLOB_RECURSE SRC "src/*.cpp")
file(GLOB_RECURSE CUDASRC "src/*.cu")
file(GLOB_RECURSE HDR "include/*.h")
list(APPEND SRC ${HDR})
list(APPEND SRC ${CUDASRC})

add_executable(${PROJECT_NAME} ${SRC})

target_link_libraries(${PROJECT_NAME} PUBLIC "printCubes")





# Pass options to NVCC
# set(
#     CUDA_NVCC_FLAGS
#     ${CUDA_NVCC_FLAGS}
#     -O3
#     -Xcompiler
#     -Wextra
#     )

# Specify binary name and source file to build it from
# cuda_add_library(
#     printCubes
#     src/printCubes.cu)
