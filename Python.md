# 开发环境搭建

## python2

```
sudo apt install python
```

## python3

```
sudo apt install python3
```

## pip

```
python -m ensurepip
sudo apt install python-pip
sudo apt install python3-pip
```

```
python -m pip install <package>
python3 -m pip install <package>
```

```
pip install --upgrade pip
pip download
pip uninstall
pip freeze # 查看虚拟环境重通过pip安装的包
pip show
pip check
pip search
pip config
pip hash
pip debug
```

## virtualenv 虚拟环境

```
pip install virtualenv
sudo apt install python3-virtualenv
virtualenv --no-site-packages <envName> // 创建一个新的虚拟环境
–version 显示当前版本号
-h, –help 显示帮助信息
-v, –verbose 显示详细信息
-q, –quiet  不显示详细信息
–clear 清空非root用户的安装，并重头开始创建隔离环境
-p PYTHON_EXE, –python=PYTHON_EXE 
-p python 环境地址 默认使用的是当前系统安装(/usr/bin/python)的python解析器 
--python=<python_exe>
从版本20开始默认值 
--no-site-packages 不使用本机已经安装的包 默认使用加上会报错
令隔离环境不能访问系统全局的site-packages目录
–system-site-packages  令隔离环境可以访问系统全局的site-packages目录
–unzip-setuptools 安装时解压Setuptools或Distribute
–relocatable 
重定位某个已存在的隔离环境。使用该选项将修正脚本并令所有.pth文件使用相当路径。 
–distribute 
使用Distribute代替Setuptools，也可设置环境变量VIRTUALENV_DISTRIBUTE达到同样效要。 
–extra-search-dir=SEARCH_DIRS 
用于查找setuptools/distribute/pip发布包的目录。可以添加任意数量的–extra-search-dir路径。 
–never-download 
禁止从网上下载任何数据。此时，如果在本地搜索发布包失败，virtualenv就会报错。 
–prompt==PROMPT 
定义隔离环境的命令行前缀


virtualenv -p <path> --no-site-packages <envName>
pip list # 查看安装的包

windows
activate 进入环境
deactivate 退出环境

ubutn
virtualenv -p /usr/bin/python3 env
source env/bin/activate 激活虚拟化环境的命令
　deactivate 当前的venv虚拟化环境



```

## Miniconda

```
Anaconda 开源的python发行版本
```

```
1. conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
2. conda config --set show_channel_urls yes

conda create -n python_3.6 python=3.6
python_3.6 名称
python=3.6 指定python版本

Anaconda promot 中需在命令前加conda
cmd中 不需在命令前加conda
conda activate python_3.6 触发刚刚创建的环境

conda deactivate 退出
activate base 切换到默认的base环境

conda install <package> 安装
pip install scikit-learn 安装
python
import pandas 检查是否安装成功
conda list 查看所有工具包
```

```

```



```

```



















# Env

python

```
python3 src.py
```

环境变量

```
PYTHONPATH 模块搜索路径
```

# 语法

```
注释
#
‘’‘ 三个单引号
“”“ 单个双引号

变量定义
<name> = <value>
del <name> # 删除变量

数据类型
数字
字符串
元组 ()
列表 []
字典 {}

运算符
算术运算符
+ 加法运算符
- 减法运算符 取反运算符
* 乘法运算符
/ 除法运算符
% 取模运算符
** 幂运算符
// 取整除运算符
逻辑运算符

比较运算符
> 大于运算符
>= 大于等于运算符
< 小于运算符
<= 小于等于运算符
== 等于运算符
!= 不等于运算符
<> 不等于运算符 python3已废弃

赋值运算符
= 简单赋值运算符
+= 加法赋值运算符
-= 减法赋值运算符
*= 乘法赋值运算符
/= 除法赋值运算符
%= 取模赋值运算符
**= 幂赋值运算符
//= 取整除赋值运算符

位运算符
& 按位与运算符
｜ 按位或运算符
^ 按位异或运算符
～ 按位取反运算符
<< 左移运算符
>> 右移运算符

逻辑运算符
and 逻辑与运算符
or 逻辑或运算符
not 逻辑非运算符

成员运算符
in
not in

身份运算符
is
is not

流程控制
分支流程
if 语句 # if elif else
循环流程
while 语句 # while else
for in 语句 # for in else
跳转流程
break 终止整个循环
continue 终止当前循环
pass 空语句
return 函数返回









```



## 函数

```
def
必备参数
关键字参数
默认参数
不定长参数
lambda 匿名函数
```

## 模块

```
import 模块导入
from import 导入模块指定部分
from import * 导入模块全部内容
```

## 包

```
__init__.py 包目录定义文件
```

## 异常处理

```
try except else
try finally
raise
```

## 类

```
class 定义类
self 类实例
继承 ()
方法重写
运算符重载

```

内置类属性

```
__dict__ 类属性
__doc__ 类文档字符串
__name__ 类名
__module__ 类所在模块
__bases__ 类所有父类
```

内置类函数

```
__init__ 构造函数
__del__ 析构函数
__repr__
__str__ 转换为字符串
__cmp__ 对象比较
```



## 接口

# Django

# Flask

# Scrapy

# NumPy

# PyTorch

