cmake_minimum_required (VERSION 2.8)
 
project (learn_cmake)

aux_source_directory(. SRC_LIST)
 
add_executable(hello ${SRC_LIST})