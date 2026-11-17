cmake -S . -B build-new -G Ninja
cmake --build build-new

只清理编译产物，保留 CMake 配置和缓存
cmake --build build --target clean


跨平台的 CMake 命令，彻底删除整个 build 文件夹
cmake -E remove_directory build
