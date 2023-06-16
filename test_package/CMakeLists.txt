cmake_minimum_required(VERSION 3.24)
project(PackageTest CUDA CXX)

find_package(CUDAToolkit REQUIRED)
find_package(conancudalib CONFIG REQUIRED)

add_executable(example src/example.cpp)
# Another workaround is to flatten the CMake targets, by directly linking to the **unsafe** internal CONAN_LIB target
# We can fix the order of libs the CMake is passing to GCC
# target_link_libraries(example PRIVATE conancudalib::conancudalib CONAN_LIB::conancudalib_conancudalib_RELEASE CUDA::cudart_static)

# Recommended: As this is a "system_lib" from Conan's perspective we can explicit depend on it from `cpp_info` and make sure it can be found
# from the linker by including this path
target_link_directories(example PRIVATE ${CUDAToolkit_LIBRARY_DIR})
target_link_libraries(example PRIVATE conancudalib::conancudalib CUDA::cudart_static)

# The last option, would be to have a system package that can find the correct paths and load that information in `cpp_info`
# the be required to include all the correct information. This could not be distributed however because of the EULA for the CUDA
# toolkit
