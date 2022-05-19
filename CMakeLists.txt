cmake_minimum_required(VERSION 3.0.0)
project(matMulVSCodeDebug VERSION 0.1.0 LANGUAGES CXX CUDA)
enable_language(CUDA)
set(CUDA_VERBOSE_BUILD ON)
find_package(CUDA REQUIRED)

#Add a sub directory where the CMakeLists.txt will be built, and a seperate scope is created. 
#For more info, https://levelup.gitconnected.com/cmake-variable-scope-f062833581b7
set(CMAKE_CUDA_FLAGS_DEBUG "-g -G")

set( CMAKE_EXPORT_COMPILE_COMMANDS ON )

add_executable(${PROJECT_NAME} matrixMul.cu)

#Download the Cuda samples and point to the Common folder (from the workingSpace)
target_include_directories(${PROJECT_NAME} PRIVATE "../cuda-samples/Common/")

set_target_properties(${PROJECT_NAME} PROPERTIES CUDA_SEPARABLE_COMPILATION ON)