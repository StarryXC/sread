# C

# 开发环境搭建

```
CLion

Main Entry int main()
```

# 命令行

```
gcc
g++
clang
```

# 语法

```
注释
// 单行注释
/* */ 多行注释

变量 变量声明 变量定义
<type> <name> = <value>;

数据类型
变量存储类型
auto
register
static
extern

运算符



















```



```
vc12-win32/x64	gcc-5.3.1 i686	gcc-5.3.1 x86_64
char			1
unsigned char	1
short			2
unsigned short	2
int				4
unsigned int	4
long			4	4	8
unsigned long	4	4	8
float			4
double			8
long int		4	4	8
long long		8
long double		8	12	16

```

## 浮点数精度

```
float		6位小数	4	1.2E-38~3.4E+38
double		15位小数	8	2.3E-308~1.7E+308
long double	19位小数	16	3.4E-4932~1.1E+4932

```

## 变量存储类型

```
auto 自动变量
	所有局部变量定义的默认类型
	只能用在函数内
	只能修饰局部变量
register 寄存器变量
	存储在寄存器中的变量
	变量的最大尺寸等于寄存器的大小
	不能使用一元的 '&' 运算符操作
	一般只用于需要快速访问的变量
	该变量不一定存于寄存器中，与硬件实现有关
static 静态类型
	修饰局部变量：在程序的生命周期内保持局部变量的存在
	修饰全局变量：使变量的作用域限制在声明它的文件内
	全局变量默认 static
extern 外部类型
	修饰的全局变量对所有程序文件可见
```

## 常量/字面量

```
const int i = 100; // 定义常量 整数字面量
// 浮点字面量
```

```
算术运算符
+ # 
- # 
* # 
/ # 
% # 
++ # 
-- # 
比较运算符
== # 
!= # 
> # 
>= # 
< # 
<= # 
逻辑运算符
&& # 
|| # 
! # 
按位运算符
& # 
| # 
~ # 
^ # 
<< # 
>> # 
赋值运算符
= # 
+= # 
-= # 
*= # 
/= # 
%= # 
&= # 
|= # 
^= # 
<<= # 
>>= # 
关系运算符 三元运算符 条件运算符
? : # 
```

指针运算符 取地址运算符

```
int i = 100;
printf("%ld \n", &i); // 取地址 586611188
int *p = &i;
printf("%ld \n", p); // 地址 586611188
printf("%ld \n", *p); // 指针 100
```

## 流程控制

分支流程

```

```

循环流程

```

```

跳转流程

```

```

## 数组

## 函数

可变参数

```

```

## 枚举

## 结构体

## 共用体

## 指针

# 预处理

## 预定义

```
#define MYDEFINE 100 // 定义常量的一种方式
```

## 文件包含

```
#include <stdio.h> // 文件包含
```

## 条件编译

```
#if // 条件编译
```

























```
c.h
#include <stdio.h>

#ifndef STARRYANDROID_JNIC_H
#define STARRYANDROID_JNIC_H

void get();

#endif //STARRYANDROID_JNIC_H
```

```
c.cpp
#include "c.h"

void get() {

}
```

格式化说明符

```
%i %d int 有符号10进制整数
%4d %04d 指定位数输出

%ld %lld 长整型

%o unsigned int 无符号8进制整数

%u unsigned int 无符号10进制整型
%lu

%x unsigned int 无符号16进制 小写 不输出前缀
%X unsigned int 无符号16进制 大写
%#x 无符号16进制 小写 输出前缀
%#X 无符号16进制 大写

%c 字符 char

%8s 字符串 char * 数组 char[] 以'\0'结尾
%6.9s 不小于6 不大于9字符串 char *
%S wchar_t *p = "tongtong" 字符串 wchar_t *

%f 单精度浮点数 6位四舍五入 double
%5.4f 单精度浮点数 6位四舍五入

%lf 双进度浮点数 同 f

%e %E 科学计数法 double

%g %G 有效位数 默认位数 double

%.4g 有效位数 指定位数

%p &pi // float pi
十六进制输出指针 void *
```

# stdio.h

```
sizeof(long long) 对象或类型存储字节大小

getc() 从一个文件读取一个字符
putc() 写一个字符到一个流
fgetc() 从流获取一个字符
fputc() 写一个字符到一个文件
ungetc() 把一个字符放回一个流
gets() 从STDIN(标准输入)读取一个字符串
puts() 写一个字符串到STDOUT(标准输出)
fgets() 从一个流获取一串字符
fputs() 写一个字符串到一个文件

getchar() 从STDIN(标准输入)读取一个字符
putchar() 写一个字符到STDOUT(标准输出)

printf() 写格式化的输出到STDOUT(标准输出)
scanf() 从STDIN(标准输入)读取格式化输入
sprintf() 写格式化的输出到缓冲区
sscanf() 从一个缓冲区读取格式化的输入
fscanf() 从一个文件读取一个格式化的输入
fprintf() 打印格式化的输出到一个文件
vprintf, vfprintf, vsprintf 写用参数列表格式化输出

fopen() 打开一个文件
freopen() 用一个不同的名称打开一个存在的流
fclose() 关闭一个文件
tmpfile() 返回一个到一个临时文件的指针
tmpnam() 返回一个独特的文件名

fseek() 在文件中移动到一个指定的位置
fsetpos() 在一个文件中移动到一个指定的位置
ftell() 返回当前文件的位置指针
rewind() 移动文件位置指针到一个文件的开始处
fgetpos() 获取文件位置指针

fwrite() 写入一个文件
fread() 从一个文件读取
fflush() 书写输出缓存的内容

setbuf() 设置一个指定流的缓冲区
setvbuf() 设置一个指定流的缓冲区和大小

clearerr() 清除错误
perror() 显示当前错误的一个字符串版本到STDERR(标准错误输出)

remove() 清除一个文件
rename() 重命名一个文件

feof() 如果到达文件尾(end-of-file)返回"True"(真)
ferror() 检查一个文件错误
```

date.h

```
difftime() 两时刻的间隔
strftime() 返回日期和时间的单个元素
asctime() 时间文本格式
clock() 返回自程序开始运行所经过的时间
ctime() 返回特定格式时间
mktime() 返回指定时间的日历格式
time() 返回系统的当前日历时间
localtime() 返回指向当前时间的指针
gmtime() 返回指向当前格林威治时间的指针
```

float.h

```
FLT_MIN 最大值
FLT_MAX 最小值
FLT_DIG 精度
```

math.h

```
log() 自然对数
log10() 以10为底的自然对数
acos() 求反余弦
asin() 求反正弦
atan() 求反正切
atan2() 求反正切，按符号判定象限
sin() 求正弦
cos() 求余弦
tan() 求正切
sinh() 求双曲正弦
cosh() 求双曲余弦
tanh() 求双曲正切
abs() 求绝对值
fabs() 求浮点数的绝对值
labs() 求长整型数的绝对值
ceil() 求不小于某值的最小整数 （求上界）
floor() 求不大于某值的最大整数 （求下界）
pow() 求幂
exp() 求e的幂
sqrt() 求平方根
div() 求商和余数
ldiv() 以长整型返回商和余数
fmod() 求模数
frexp() 求数的科学表示法形式
ldexp() 以科学计数法计算
modf() 将一个数分解成整数和小数部分
```

mem.h

```
calloc() 分配一个二维储存空间
free() 释放已分配空间
malloc() 分配空间
realloc() 改变已分配空间的大小
```

freetype.h

# C++

# Env

gcc

```
gcc main.c *.c -o main.out
```

main

```
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

```
cmake_minimum_required(VERSION 3.13)
project(untitled)

set(CMAKE_CXX_STANDARD 14)

add_executable(untitled main.cpp)
```

## 注释

## 变量

## 运算符

算术运算符

逻辑运算符

关系运算符

比较运算符

赋值运算符

条件运算符

指针运算符

## 流程控制

分支流程

循环流程

跳转流程

## 函数

可变参数函数

## 数组

# 预处理指令

## 宏定义

## 文件包含

## 条件编译

# FFmpeg

# Env

```
http://ffmpeg.zeranoe.com/builds/

Static 静态库 应用程序
bin
    ffmpeg.exe
    ffplay.exe
    ffprobe.exe
doc
presets

Shared 共享库
bin
    avcodec-58.dll
    avdevice-58.dll
    avfilter-7.dll
    avformat-58.dll
    avutil-56.dll
    postproc-55.dll
    swresample-3.dll
    swscale-5.dll
    ffmpeg.exe
    ffplay.exe
    ffprobe.exe
doc
presets

Dev 开发
lib
include
    libavcodec
    libavdevice
    libavfilter
    libavformat
    libavutil
    libpostproc
    libswresample
    libswscale
examples

```

## VS FFmpeg配置

## Qt FFmpeg配置

## CLion FFmpeg配置

# OpenCV

```
brew install opencv
```

# OpenGL

# 窗口库

```
SDL
GLFW
GLUT
```

# Boost

# Cocos2d

# srs



