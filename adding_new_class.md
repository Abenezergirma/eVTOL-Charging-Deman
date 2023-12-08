# Integration of a New Class into a C++ Project Using CMake

## Overview
This document details the process of adding a new C++ class to an existing project (`user.cxx`), which utilizes the PSOPT library, and configuring the build process using CMake.

## Steps

### 1. Class Creation
- A new class `ExperimentalSettings` was created to manage experimental settings for PSOPT-based simulations.
- The class was divided into two files: `ExperimentalSettings.h` (header file) and `ExperimentalSettings.cxx` (implementation file).

### 2. Modifying `CMakeLists.txt`
- The `CMakeLists.txt` file in the `user` subdirectory under the `examples` directory was updated to include the new class in the build process.
- The `add_executable` command was modified to compile both `user.cxx` and `ExperimentalSettings.cxx`.

    ```cmake
    add_executable(${PROJECT_NAME} user.cxx ExperimentalSettings.cxx)
    ```

### 3. Linking Dependencies
- Used `target_link_libraries` to link necessary libraries including `libPSOPT.a`, IPOPT, ADOL-C, and Eigen3.
- Specified the paths to the libraries in the `target_link_libraries` command.

### 4. Resolving Include Paths
- Added include paths for PSOPT header files using `include_directories`.
- Specified the path to the directory containing `psopt.h`.

    ```cmake
    include_directories("/path/to/psopt/include")
    ```

### 5. Configuring IPOPT and Eigen3
- Configured IPOPT and Eigen3 within the CMake environment using `find_package`.
- Set up IPOPT package with `pkg_check_modules`.

    ```cmake
    find_package(PkgConfig REQUIRED)
    pkg_check_modules(ipopt REQUIRED IMPORTED_TARGET ipopt)
    find_package(Eigen3 REQUIRED)
    ```

### 6. Running CMake
- Created a `build` directory for an out-of-source build.
- Ran CMake to generate the build system:

    ```bash
    cmake ..
    ```

### 7. Compiling the Project
- Compiled the project using `make`:

    ```bash
    make
    ```

### 8. Troubleshooting Compilation Errors
- Iteratively resolved various compilation errors:
    - Missing `psopt.h` file issues were addressed by setting the correct include path.
    - Problems with finding IPOPT and Eigen3 were solved by proper configuration in `CMakeLists.txt`.

## Conclusion
This documentation illustrates the integration of a new class into an existing C++ project using CMake, ensuring all dependencies and paths are correctly configured. It highlights the importance of iterative troubleshooting in resolving compilation errors.

