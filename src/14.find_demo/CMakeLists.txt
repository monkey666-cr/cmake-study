cmake_minimum_required(VERSION 3.10)

project(find_demo)

add_executable(${PROJECT_NAME} main.cpp)

#[[
使用find_package寻找<LibaryName>库，如果找到，有以下变量
<LibaryName>_FOUND：表示是否找到
<LibaryName>_INCLUDE_DIR：表示头文件目录
<LibaryName>_LIBRARIES：表示库文件目录
]]

# 寻找gflags库, REQUIRED表示必须存在, 否则报错
find_package(gflags REQUIRED)

if (gflags_FOUND)
    message(STATUS "gflags found")
    message(STATUS "gflags include dir: ${gflags_INCLUDE_DIR}")
    message(STATUS "gflags lib dir: ${gflags_LIBRARIES}")

    target_include_directories(find_demo PRIVATE ${gflags_INCLUDE_DIR})
    target_link_libraries(find_demo ${gflags_LIBRARIES})
else()
    message(FATAL_ERROR "gflags not found")
endif()