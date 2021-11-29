# QTemplate
This is a template project for QT Creator.
<br>
I created this project for those who want to work with the QT framework in VS Code/Visual Studio.
<br>
The main feature of this project is that it makes the code source generate by QT more esily to mantain. I also rewrote the CMakeLists.txt to be more easy to add external libraries in the future.

# Programs and libraries hosted in this solution
- [Visual Studio Community](https://www.visualstudio.com/) v2022
- [QT Creator](https://www.qt.io/) v5.15.2

For this project to compile, you will need to **install Desktop Qt 5.15.2 MSVC2019 64bit Kit** and to put it in the **environment variables path**

# Supported platforms / recommended toolchains
The following are recommended toolchains for popular platforms.
- Windows -- [Visual Studio](https://www.visualstudio.com/) (Microsoft Visual C++)
- QT Creator

# Building
There are two distinct steps in the build process:
1. Generation of the build system, using CMake   
2. Compiling, linking, etc., using CMake-compatible toolchain

# Prerequisites
- [CMake](https://cmake.org/) version 3.8 or newer
- C++17 toolchain compatible with CMake for your development platform (e.g. [Visual Studio](https://www.visualstudio.com/) on Windows)
- [QT Creator](https://www.qt.io/) v5.15.2

# How to install
```bash
git clone https://github.com/vasilecampeanu/QTemplate.git
```

# Build system generation 
```bash
mkdir build
cd build
cmake -G "Visual Studio 17 2022" -A "x64" ..
```

# Compiling, linking ...
```bash
cd build
cmake --build . --config Debug
```