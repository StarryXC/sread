# 开发环境搭建

```
apt install php7.4-cli

apt install php
apt install libapache2-mod-php
apt install php7.0-mysql
apt install phpmyadmin
```

服务操作

```
service apache2 restart
service mysql restart
service php7.0-fpm restart
```

apache2.conf

```
末尾添加
include /etc/phpmyadmin/apache.conf

AddType applicatin/x-httpd-php .php .html .htm

AddDefaultCharset UTF-8

访问 http://localhost/phpmyadmin/
```



## 命令行

### php

```
php -v
```

# 语法

## 基础语法

```
注释
// 单行注释
/* */ 多行注释

变量
$<name> = <value>;
数据类型
"" '' # 字符串
100 # 整型
100.0 # 浮点型
数组

运算符
算术运算符
+
-
*
/
%
++
--
逻辑运算符
and
or
xor
&&
||
!
关系运算符 条件
? : # 
比较运算符
>
>=
<
<=
==
!= <>
===
!==
赋值运算符
=
+=
-=
*=
/=
%=
.=

并置运算符
. # 连接字符串
数组运算符
+
==
!= <>
===
!==
流程控制
分支流程
if # if elseif else
switch # switch case default
循环流程
for # for
foreach # foreach as
while # while
do while # do while
跳转流程
```

### 函数

## 面向对象语法

### 类

### 接口

# 超级全局变量





















