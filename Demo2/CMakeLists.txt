#最低版本
cmake_minimum_required(VERSION 2.8)
# 项目名称
project(learn_cmake)
#引入头文件路径
include_directories(./inc_dir1 ./inc_dir2)
#获取某目录下的所有源文件
aux_source_directory(./src_dir1 SRC_LIST1)
aux_source_directory(./src_dir2 SRC_LIST2)
aux_source_directory(main_dir MAIN_DIR)
#生成可执行文件
add_executable(hello ${SRC_LIST1} ${SRC_LIST2} ${MAIN_DIR})