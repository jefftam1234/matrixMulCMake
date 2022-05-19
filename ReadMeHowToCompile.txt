1. set the environment variable
set cuda software_preemption on
export CUDA_DEBUGGER_SOFTWARE_PREEMPTION=1


2. using CMake

{
cmake_minimum_required(VERSION 3.0.0)
project(JTCudaLib VERSION 0.1.0 LANGUAGES CXX CUDA)
enable_language(CUDA)
set(CUDA_VERBOSE_BUILD ON)
find_package(CUDA REQUIRED)

#Add a sub directory where the CMakeLists.txt will be built, and a seperate scope is created. 
#For more info, https://levelup.gitconnected.com/cmake-variable-scope-f062833581b7
set(CMAKE_CUDA_FLAGS_DEBUG "-g -G")

set( CMAKE_EXPORT_COMPILE_COMMANDS ON )

add_executable(${PROJECT_NAME} matrixMul.cu)

target_include_directories(${PROJECT_NAME} PRIVATE "../../../Common/")

set_target_properties(${PROJECT_NAME} PROPERTIES CUDA_SEPARABLE_COMPILATION ON)
}

mkdir build
cmake -DCMAKE_BUILD_TYPE=Debug -S . -B ./build

3. build the binary
in the build folder

make dbg=1
file ./JTCudaLib
(see if it can find debug symbols in the file)
set break point in kernel
and run, if everything goes right it should stop at the breakpoint

4. setup VSCode environment (IDE)
in c_cpp_properties.json add this line in the configuration:     
    "compileCommands": "${workspaceFolder}/build/compile_commands.json",

in launch.json (if not created, do it first)
point to the binary:

"program": "${workspaceFolder}/build/JTCudaLib"

set breakpoint and it should stops as well, congrats you can now debug CUDA code in VSCode