#最低版本号
cmake_minimum_required(VERSION 3.0)

# 项目名称

project(learn_lib)

# 整合源文件
aux_source_directory(${PROJECT_BINARY_DIR}/../main_src MAIN_SRC)

#引入头文件路径
include_directories(${PROJECT_BINARY_DIR}/../inc)

 #查找库文件，第二个参数:要查找的库文件，第三个参数:要在那个目录下查找
 #第一个参数:是一个变量，用于储存查找到的库文件
find_library(FUNC_LIB myfunc ${PROJECT_BINARY_DIR}/../lib)

#设置可执行文件生成到哪里
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/../bin)

#生成可执行文件
add_executable(hello ${MAIN_SRC})
# 把库链接到可执行文件中
target_link_libraries(hello ${FUNC_LIB})