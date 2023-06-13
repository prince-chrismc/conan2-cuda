cmake_minimum_required(VERSION 3.24)
project(PackageTest CUDA CXX)

find_package(CUDAToolkit REQUIRED)
find_package(conancudalib CONFIG REQUIRED)

add_executable(example src/example.cpp)
# target_link_libraries(conancudalib::conancudalib INTERFACE CUDA::cudart_static)
target_link_libraries(example PRIVATE conancudalib::conancudalib CUDA::cudart_static)
