> Thinking

```
cmake_minimum_required
project
add_executable
```

> Memory

```
cmake_minimum_required(VERSION 3.13)
project(untitled)
set(CMAKE_CXX_STANDARD 14)
add_executable(untitled main.cpp)


cmake_minimum_required(VERSION 3.4.1)
#设置变量
set(OpenCV_DIR E:/opencv-3.4.2-android-sdk/OpenCV-android-sdk/sdk/native/jni)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11") #支持-std=gnu++11
find_package(OpenCV REQUIRED)

#判断编译器类型,如果是gcc编译器,则在编译选项中加入c++11支持
if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
    message(STATUS "optional:-std=c++11")
endif(CMAKE_COMPILER_IS_GNUCXX)
${CMAKE_SOURCE_DIR}
target_include_directories(
                            dxtx
                            PRIVATE
                            E:/opencv-3.4.2-android-sdk/OpenCV-android-sdk/sdk/native/jni/include
                            src/main/jni/include
                            )

add_library( 
             native-lib # 名称
             
             SHARED # 类型
             
             src/main/cpp/JNIc.cpp # 原文件路径
             src/main/cpp/JNIc.h
              )

add_library(freetype STATIC IMPORTED)
set_target_properties(freetype  PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/obj/local/${ANDROID_ABI}/libft2.a)

find_library( # 名称
              log-lib
              # 库名称
              log )
include_directories(src/main/jniLibs/include)
target_link_libraries( # 目标库
                       native-lib
                       # 链接库
                       ${log-lib} )
target_link_libraries(
                        dxtx freetype
                       ${OpenCV_LIBS}
                       ${Log-lib} )
```

