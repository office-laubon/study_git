# 指定本工程要求的最低 CMake 版本。
cmake_minimum_required(VERSION 3.16)

# 定义工程名称、版本以及使用的编程语言（CXX 表示 C++）。
project(hello_world VERSION 1.0 LANGUAGES CXX)

# 使用 C++17 标准，并要求编译器必须支持该标准。
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 关闭编译器特有的语言扩展，使代码更符合标准、更容易跨平台。
set(CMAKE_CXX_EXTENSIONS OFF)

# 把生成的可执行程序统一放到 build/bin 目录。
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

# Visual Studio 等多配置生成器会区分 Debug、Release 等模式。
# 下面的设置保证所有模式的可执行程序都输出到同一个 bin 目录。
foreach(config Debug Release RelWithDebInfo MinSizeRel)
    string(TOUPPER "${config}" config_upper)
    set("CMAKE_RUNTIME_OUTPUT_DIRECTORY_${config_upper}" "${CMAKE_BINARY_DIR}/bin")
endforeach()

# 创建名为 hello 的可执行程序，并指定参与编译的源文件。
add_executable(hello src/main.cpp)

# 根据编译器类型开启较严格的警告检查。
if(MSVC)
    # Microsoft Visual C++ 编译器选项。
    target_compile_options(hello PRIVATE /W4 /permissive-)
else()
    # GCC 或 Clang 编译器选项。
    target_compile_options(hello PRIVATE -Wall -Wextra -Wpedantic)
endif()
