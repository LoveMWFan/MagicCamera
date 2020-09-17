cmake_minimum_required(VERSION 3.4.1)

# 支持gnu++11
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")


# 查找代码中使用到的系统库
find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# 配置目标so库编译信息
add_library( # Sets the name of the library.
        MagicBeautify

        # Sets the library as a shared library.
        SHARED

        ${CMAKE_SOURCE_DIR}/beautify/MagicBeautify.cpp
        ${CMAKE_SOURCE_DIR}/beautify/MagicBeautify.h
        ${CMAKE_SOURCE_DIR}/bitmap/BitmapOperation.cpp
        ${CMAKE_SOURCE_DIR}/bitmap/BitmapOperation.h
        ${CMAKE_SOURCE_DIR}/bitmap/Conversion.cpp
        ${CMAKE_SOURCE_DIR}/bitmap/Conversion.h
        ${CMAKE_SOURCE_DIR}/bitmap/JniBitmap.h
        ${CMAKE_SOURCE_DIR}/MagicJni.cpp
        )

# 指定编译目标库时，cmake要链接的库
target_link_libraries(

        # 指定目标库，native-lib 是在上面 add_library 中配置的目标库
        MagicBeautify

        -landroid
        -lEGL
        -lGLESv2
        jnigraphics
        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})