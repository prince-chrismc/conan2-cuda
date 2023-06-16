# conan2-cuda-lib-experience
Test of creating a library depending on cuda Toolkit using Conan 2.0 Package Manager


## Instructions

From this repo cloned locally,

```bat
conan config home
conan config install .conan
REM Note: i have CMake installed so I used the system tools not avoid the download
conan create . -pr vs2022
```

I've install Visual Studio 2022, CMake, and CUDA dev kit.

For getting  it in WSL, I used the CUDA deb installer + needed to add the compiler to the path
