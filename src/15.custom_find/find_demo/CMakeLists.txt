cmake_minimum_required(VERSION 3.10)
 
project(main)

# 设置 CMAKE_MODULE_PATH 让find_package查找
SET(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake)
message("CMAKE_MODULE_PATH: ${CMAKE_MODULE_PATH}")

# 设置一个缓存变量
SET(DLIB_INSTALL_PATH "./" CACHE PATH "dlib的安装路径")
message(STATUS "dlib的安装路径为: ${DLIB_INSTALL_PATH}")

# 查找自定义的包
find_package(dlib REQUIRED)

if (dlib_FOUND)
    message("dlib found")
    message("dlib include dir: ${dlib_INCLUDE_DIR}")
    message("dlib lib: ${dlib_LIBRARY}")
    message("dlib version: ${dlib_VERSION}")
    message("dlib author: ${dlib_AUTHOR}")
    message("dlib lib dir: ${dlib_LIBRARY_DIR}")
else()
    message("dlib not found")
endif()

# 设置RPATH
SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
SET(CMAKE_INSTALL_RPATH "${dlib_LIBRARY_DIR}")

add_executable(main main.cpp)

target_include_directories(main PUBLIC ${dlib_INCLUDE_DIR})
target_link_libraries(main ${dlib_LIBRARY})

install(
    TARGETS main
    RUNTIME DESTINATION bin
)

#[[
CMAKE_INSTALL_PREFIX为安装路径（系统内置），DLIB_INSTALL_PATH为dlib安装路径

cmake -S . -B build -DCMAKE_INSTALL_PREFIX=../installed -DDLIB_INSTALL_PATH=../installed

cmake --build build
cmake --install build

]]
