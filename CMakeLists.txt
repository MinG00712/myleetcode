cmake_minimum_required(VERSION 3.22)
project(leetcode)

set(CMAKE_CXX_STANDARD 17)

# 设置输出目录为 bin/
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# 扫描源代码目录下的所有 .cpp 文件
file(GLOB_RECURSE SRC_FILES "src/*.cpp")

# 扫描头文件目录下的所有 .h 文件
file(GLOB_RECURSE HEADER_FILES "include/*.h")

# 遍历每对同名的 .cpp 和 .h 文件，生成可执行文件
foreach(SRC_FILE ${SRC_FILES})
    # 提取文件名（不包含路径和扩展名）
    get_filename_component(EXEC_NAME ${SRC_FILE} NAME_WE)

    # 查找对应的 .h 文件
    foreach(HEADER_FILE ${HEADER_FILES})
        get_filename_component(HEADER_NAME ${HEADER_FILE} NAME_WE)
        if(HEADER_NAME STREQUAL EXEC_NAME)
            # 找到同名的 .h 文件，生成可执行文件
            add_executable(${EXEC_NAME} ${SRC_FILE} ${HEADER_FILE})
        endif()
    endforeach()
endforeach()