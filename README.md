CMake 是一个开源的跨平台构建系统，它通过使用平台无关的配置文件来生成特定平台的构建文件，如 Unix 的 `Makefile` 或 Windows 的 Visual Studio 项目文件。CMake 尤其适合管理大型的 C/C++ 项目，并在跨平台项目中广泛应用。以下是 CMake 的基本概念和用法介绍。

### 1. **CMake 基本概念**

CMake 的核心文件是 `CMakeLists.txt`，它定义了项目的构建规则，包含了源文件、目标可执行文件或库、编译选项等信息。CMake 会根据这些规则生成适合目标平台的构建文件。

### 2. **CMake 使用步骤**

#### 第一步：创建 `CMakeLists.txt`

在项目的根目录下创建一个 `CMakeLists.txt` 文件，并写入以下基本内容：

```cmake
# 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目名称
project(MyProject)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 11)

# 添加可执行文件
add_executable(MyExecutable main.cpp)
```

- `cmake_minimum_required(VERSION 3.10)`：指定最低 CMake 版本。
- `project(MyProject)`：定义项目名称。
- `set(CMAKE_CXX_STANDARD 11)`：设置 C++ 标准（例如 C++11）。
- `add_executable(MyExecutable main.cpp)`：定义一个可执行文件，`main.cpp` 是源文件。

#### 第二步：生成构建文件

在项目根目录下创建一个 `build` 目录，用于存放生成的构建文件：

```bash
mkdir build
cd build
cmake ..
```

运行 `cmake ..` 命令后，CMake 会在 `build` 目录中生成构建文件。如果是在 Unix 系统上，生成的是 `Makefile`；在 Windows 上，生成的是 Visual Studio 项目文件。

#### 第三步：构建项目

在 `build` 目录下运行以下命令开始编译项目：

```bash
cmake --build .
```

这会调用生成的构建文件来编译项目，生成的可执行文件或库文件会输出到 `build` 目录中。

### 3. **常用的 CMake 指令**

- **`add_library`**：定义一个库目标，可以是静态库或动态库。例如：

  ```cmake
  add_library(MyLibrary STATIC mylib.cpp)
  ```

- **`target_include_directories`**：指定头文件目录。例如：

  ```cmake
  target_include_directories(MyExecutable PRIVATE include)
  ```

- **`target_link_libraries`**：为目标文件指定要链接的库。例如：

  ```cmake
  target_link_libraries(MyExecutable PRIVATE MyLibrary)
  ```

- **`find_package`**：寻找已安装的包并链接到项目中。例如，使用 `find_package` 查找并链接 Boost 库：

  ```cmake
  find_package(Boost REQUIRED)
  target_link_libraries(MyExecutable PRIVATE Boost::Boost)
  ```

### 4. **CMake 高级功能**

- **条件编译**：可以根据平台或编译选项条件性地包含源文件或设置变量。例如：

  ```cmake
  if (WIN32)
    # Windows-specific settings
  elseif (UNIX)
    # Unix-specific settings
  endif()
  ```

- **外部依赖管理**：通过 `FetchContent` 下载和管理外部库。例如：

  ```cmake
  include(FetchContent)
  FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/release-1.10.0.zip
  )
  FetchContent_MakeAvailable(googletest)
  ```

CMake 是一个功能丰富的工具，通过其模块化配置和跨平台支持，能够有效管理复杂的 C++ 项目。
