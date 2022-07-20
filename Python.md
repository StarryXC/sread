# Python

## 环境搭建

```
python2
sudo apt install python

python3
sudo apt install python3

环境变量
PYTHONPATH 模块搜索路径
```

## 命令行

```
python
pip
```

```
python
python3 src.py
python -m ensurepip
sudo apt install python-pip
sudo apt install python3-pip

python -m pip install <package>
python3 -m pip install <package>

pip
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

```
virtualenv 虚拟环境
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

Miniconda
Anaconda 开源的python发行版本

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
# coding=UTF-8

# 注释函数
def myCommonts:
    myInt

    myList



myInt = 100
myInt, myString = 200, "myString"

myList = [1, 2, 3, 4, 5]
print(myList)
print(myList[2])
print(myList[0:3])
print(myList[0:3:2])
print(myList * 3)
print(myList + [1, 2])

myTuple = (1, 2, 3, 4, 5)
print(myTuple)
print(myTuple[2])
print(myTuple[0:3])
print(myTuple[0:3:2])
print(myTuple * 3)
print(myTuple + (1, 3))

myDict = {}
myDict[1] = 'a'
myDict['a'] = 23
myDict = {1: 'a', 'a': 24}
print(myDict)
print(myDict[1])
print(myDict['a'])
print(myDict.keys())
print(myDict.values())


myInt = 10
if myInt == 1:
    print(myInt)
elif myInt == 3:
    print(myInt)
else:
    print(myInt)

myString = "string"
myString.lstrip()
myString.rstrip()
print(myString[2])
print(myString[0:3])
print(myString[0:4:2])
print(myString * 2)
print(myString + "age")

while myInt == 10:
    print(myInt)
    myInt = myInt + 1
else:
    print(myInt)

while 1:
    if myInt == 4:
        print(myInt)
        break
    myInt = myInt - 1

for char in myString:
    print(char)
else:
    print(char)

for i in range(len(myString)):
    print(myString[i])


def myDef(x, y, z=10, *var):
    print(x)
    print(y)
    print(z)
    for i in var:
        print(i)
    return 10
myDef(10, 10)
myDef(10, 10, 20)
myDef(z=10, y=10, x=20)
myDef(1, 1, 1, 1, 1)

myLambda = lambda x, y, z: x+y+z
print(myLambda(1, 2, -1))

class MyClass:
    myInt = 100

    def __init__(self, myInt):
        print(self)
        self.myInt = myInt
    def myDef(self):
        print(self)

MyClass.myInt = 200
print(MyClass.myInt)
print(MyClass.__dict__)
print(MyClass.__doc__)
print(MyClass.__name__)
print(MyClass.__module__)
print(MyClass.__bases__)

print(MyClass.__dict__)
print(MyClass.__dict__)

myClass = MyClass(12)
print(myClass.__class__)
print(myClass.myDef())

del myClass.myInt

print(hasattr(myClass, 'myInt'))
print(getattr(myClass, 'myInt'))
print(setattr(myClass, 'myInt', 100))
delattr(myClass, 'myInt')


class MySuperClass:
    myInt = 100

    def __init__(self):
        print('super init')

    def my_def(self):
        print('super myDef')

class MyChildClass(MySuperClass):

    myInt = 300
    _myProtected = 100
    __myPrivate = 200

    def _myProtected(self):
        print('_myProtected')
    def __myPrivateDef(self):
        print('__myPrivateDef')

    def my_def(self):
        print('my_def')
        self.__myPrivate()
        print('child')

# myChildClass = MyChildClass()
# myChildClass.my_def()
# print(myChildClass.myInt)
# print(myChildClass._myProtected)

myStr = str("string")
print(myStr)
print(myStr.find("a") == -1)

myBool = False
if not myBool:
    print(not myBool)
if myBool and myBool:
    print(myBool)
if myBool or myBool:
    print(myBool)

myBool = 1 == ""

# continue

# from com.android.monkeyrunner import MonkeyRunner,MonkeyDevice,MonkeyImage
# from com.android.monkeyrunner.recorder import MonkeyRecorder as recorder


try:
    print('')
except IndexError:
    print('')

while (1 < 2):
    pass

if device is None:
    print('')
else:
    print('')


import random # 随机数模块
import sys # 系统模块
import time # 时间模块
import os

os.popen("adb shell uiautomator dump & adb pull /sdcard/window_dump.xml F:\\")
#下载当前布局，并回传到本机的F盘根目录，这个时候就可以查看布局坐标了

intv = random.randint(0, 720)






# coding=UTF-8

#twisted
# python 交互器模式
#
# Python 3.0 再 2.6 之后发布 不兼容 2.x，后发布2.7 兼容 2.x 和 3.x
#
# 硬盘转速
# 5400转
# 7200转
# 10000转
# 15000转


# monkeyrunner ioc.py > D:/log.txt
from com.android.monkeyrunner import MonkeyRunner,MonkeyDevice,MonkeyImage
from com.android.monkeyrunner.recorder import MonkeyRecorder

# MonkeyDevice 根据坐标操作
# EasyMonkeyDevice 通过控件id操作  手机上须启动View Server的客户端与其进行socket通信 商业手机无法开启View Server 只能运行在虚拟机或者开发机中

device = MonkeyRunner.waitForConnection()
if device is None:
    print('device is none')

# 安装 apk
device.installPackage('F:/test1/biugo.apk')
# 卸载应用
device.removePackage('com.jd.app.reader')

# 启动应用
device.startActivity(component='com.jd.app.reader/com.jingdong.app.reader.logo.JdLogoActivity')

# 保持手机唤醒
device.wake()

# 手机重启
device.reboot()

# 休眠 10 秒
MonkeyRunner.sleep(10)
MonkeyRunner.sleep(10, 0) # 0 可省略

# 手机截屏
image = device.takeSnapshot()
image.writeToFile('D:\TEST.png','png')

device.drag((100,1053),(520,1053),1.5,10)
# 滑动事件 开始坐标；结束坐标；持续时间/秒，默认1秒；插值点时要采取的步骤，默认值是10
device.touch(500, 500, 'DOWN')
# DOWN_AND_UP 触摸事件
device.type('helloworld') # 键盘输入
device.press('KEYCODE_ENTER')
# 按键事件
device.press('KEYCODE_MENU', 'DOWN_AND_UP')
device.press('KEYCODE_BACK', MonkeyDevice.DOWN_AND_UP)
# KEYCODE_BACK 返回按键
# KEYCODE_MENU 菜单按键
# KEYCODE_HOME HOME键
# KEYCODE_CALL send键
# KEYCODE_ENDCALL end键
#
# KEYCODE_DPAD_RIGHT 右导航键
# KEYCODE_DPAD_LEFT 左导航
# KEYCODE_DPAD_DOWN 下导航键
# KEYCODE_DPAD_UP 上导航键
# KEYCODE_DPAD_CENTER OK键
# KEYCODE_VOLUME_UP 上音量键
# KEYCODE_VOLUME_DOWN 下音量键
# KEYCODE_POWER power键
# KEYCODE_CAMERA camera键

# MonkeyDevice.DOWN_AND_UP
# device.touch(909,1620,u'DOWN_AND_UP')
MonkeyRecorder.start(device)



```



## 注释

```
#
‘’‘ 三个单引号
“”“ 单个双引号
```

## 变量定义

```
删除变量
<name> = <value>
del <name> # 删除变量
```

## 数据类型

```
数字
字符串
元组 ()
列表 []
字典 {}
```

## 运算符

```
算术运算符 + - * / % ** //
逻辑运算符
比较运算符 > >= < <= == != <> python3已废弃
赋值运算符 = += -= *= /= %= **= //=
位运算符 & ｜ ^ ～ << >>
逻辑运算符 and or not
成员运算符
in
not in
身份运算符
is
is not
```

## 流程控制

```
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



## 异常处理

```
try except else
try finally
raise
```

## 数据库

```

```

## 类

```
内置类属性
__dict__ 类属性
__doc__ 类文档字符串
__name__ 类名
__module__ 类所在模块
__bases__ 类所有父类

内置类函数
__init__ 构造函数
__del__ 析构函数
__repr__
__str__ 转换为字符串
__cmp__ 对象比较

class 定义类
self 类实例
继承 ()
方法重写
运算符重载
```

## 模块

```
import 模块导入
from import 导入模块指定部分
from import * 导入模块全部内容
```

## 包

```
包
__init__.py 包目录定义文件
```

## 接口

```

```

```

```

```

```

# 爬虫

```

```

# Django

```

```

```

```

```

```

# Flask

```

```

```

```

```

```

# Scrapy

```

```

```

```

```

```

# NumPy

```

```

# PyTorch

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

