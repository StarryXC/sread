# C

## Main Entry

```
int main() // std::cout << "Hello, World!" << std::endl;

```

## 命令行

```
gcc
    gcc main.c *.c -o main.out
g++
clang
```



## 注释

```
// 单行注释
/* */ 多行注释
```

## 变量定义

```
<type> <name> = <value>;
```

## 数据类型

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


浮点数精度
float		6位小数	4	1.2E-38~3.4E+38
double		15位小数	8	2.3E-308~1.7E+308
long double	19位小数	16	3.4E-4932~1.1E+4932

常量/字面量
const int i = 100; // 定义常量 整数字面量
// 浮点字面量
```

## 变量存储类型

```
变量存储类型
    auto
    register
    static
    extern
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

## 运算符

```
算术运算符 + - * / % ++ --
比较运算符 > >= < <= == !=
逻辑运算符 && || !
按位运算符 & | ~ ^ << >>
赋值运算符 = += -= *= /= %= &= |= ^= <<= >>=
关系运算符 三元运算符 条件运算符 ? :
指针运算符 取地址运算符
int i = 100;
printf("%ld \n", &i); // 取地址 586611188
int *p = &i;
printf("%ld \n", p); // 地址 586611188
printf("%ld \n", *p); // 指针 100
```

## 流程控制

```
分支流程
循环流程
跳转流程
```

## 函数

```

```

```

```

```

```

```

```

```

```



## 预定义

```
#define
```

## 文件包含

```
#include
```

## 条件编译

```
#if
#ifndef #endif
```

## 日期时间

```
date.h
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

## 数学计算

```
math.h
    自然对数 log
    以10为底的自然对数 log10
    反余弦 acos
    反正弦 asin
    反正切 atan
    反正切，按符号判定象限 atan2
    正弦 sin
    余弦 cos
    正切 tan
    双曲正弦 sinh
    双曲余弦 cosh
    双曲正切 tanh
    绝对值 abs
    浮点数绝对值 fabs
    长整型数绝对值 labs
    不小于某值的最小整数 （求上界） ceil
    不大于某值的最大整数 （求下界） floor
    求幂 pow
    e的幂 exp
    平方根 sqrt
    商和余数 div
    以长整型返回商和余数 ldiv
    模数 fmod
    数的科学表示法形式 frexp
    科学计数法计算 ldexp
    一个数分解成整数和小数部分 modf
```

## 浮点计算

```
float.h
    最大值 FLT_MIN
    最小值 FLT_MAX
    精度 FLT_DIG
```

## 内存分配

```
calloc() 分配一个二维储存空间
free() 释放已分配空间
malloc() 分配空间
realloc() 改变已分配空间的大小
```

## 输入输出

```
stdio.h
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



```

```

```

```

```

```

```

```

```

```

```

```



# C++

## 预定义

```
C/预定义
```

## 文件包含

```
C/文件包含
```

## 条件编译

```
C/条件编译
```

## 输入输出

```
iostream
```

## 类

```

```

```

```

```

```

```

```

```

```

# OC

## Main Entry

```

```

## clang

```

```



## 运算符

```
算术运算符
逻辑运算符
关系运算符
比较运算符
赋值运算符
```

## 流程控制

```
分支流程
循环流程
跳转流程
```

## 数组

```
    NSArray
    NSMutableArray
```

## 方法

```

```

## 类

```
#import @import
@interface @end
@implementation @end

属性
@property
    nonatomic
    retain
    assign
@synthesize

继承
NSObject
	release
	(void)dealloc
NSString *string = NSString string];

```

## 协议

```

```

# Foundation

```
NSObject
```

```
NSInteger
```

```

```



## 预定义

```
C/预定义
```

## 文件包含

```
C/文件包含
```

## 条件编译

```
C/条件编译
```

## Json

```

```

## 正则表达式

```

```

```

```

# C#

## Main Entry

```

```



```

```

```

```

```

```

```

```

```

```



## 注释

```
// /* */
```

## 变量定义

```
<type> <name>;
```

## 运算符

```
算术运算符 + - * / % ++ --
逻辑运算符 && || !
关系运算符 > >= < <= == !=
比较运算符
赋值运算符 = += -= *= /= %= &= |= ^= <<= >>=
按位运算符 & | ~ ^ << >>
```

## 流程控制

```
分支流程
if # if else
switch # switch case default
循环流程
for # for
foreach in # foreach in
while # while
do while # do while
跳转流程
break continue return
```

## 类

```

```

## 接口

```

```

## 委托

```

```

## 命名空间

```

```

```

```



# FFmpeg

```
VS FFmpeg配置
Qt FFmpeg配置
CLion FFmpeg配置
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

# OpenCV

```
brew install opencv
```

# OpenGL

```
窗口库
    SDL
    GLFW
    GLUT
```

# SDL

```

```

# GLFW

```

```

# GLUT

```

```

# Boost

```

```

# Cocos2d

```

```

# srs

```

```

# RTMPDump

```
http://rtmpdump.mplayerhq.hu/download/
```

#### freetype.h

```

```

# Qt

```
qtcreator http://download.qt.io/archive/qt/
https://dev.mysql.com/downloads/mysql/
```

# Unity3D

```

```

```

```

```

```

```

```



```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

