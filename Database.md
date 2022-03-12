# 数据库



# MySQL

## 环境配置

```
Windows: MySQL

net stop mysql
net start mysql

配置文件
my.ini
[mysqld]
skip-grant-tables
basedir = D:\SoftWare\MySQL\mysql-5.7.11-winx64
datadir = D:\SoftWare\MySQL\mysql-5.7.11-winx64\Data
port = 3306
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

Ubuntu
安装MySQL
sudo apt-get install mysql-server
sudo mysql_secure_installation // 初始化配置
sudo apt-get remove mysql-server // 写在mysql
sudo apt-get autoremove // 移除其他跟随mysql安装的包
sudo apt-get remove package-name // 写在其他组件
dpkg -l | grep mysql | grep ii // 查看安装列表

卸载MySQL
sudo rm /var/lib/mysql/ -R
sudo rm /etc/mysql/ -R
sudo apt-get autoremove mysql* --purge



安装目录
/usr/bin                 客户端程序和脚本  
/usr/sbin                mysqld 服务器  
/var/lib/mysql           日志文件，数据库  ［重点要知道这个］  
/usr/share/doc/packages  文档  
/usr/include/mysql       包含( 头) 文件  
/usr/lib/mysql           库  
/usr/share/mysql         错误消息和字符集文件  
/usr/share/sql-bench     基准程序

配置文件
/etc/mysql/my.cnf // 指出实际配置文件位置
/etc/mysql/my.conf // 老版本
/etc/mysql/mysql.cnf
/etc/mysql/mysql.conf.d/mysql.cnf
/etc/mysql/mysql.conf.d/mysqld.cnf // 实际配置信息
/etc/mysql/conf.d/mysql.cnf
/etc/mysql/conf.d/mysqldump.cnf
/etc/mysql/debian.cnf // 保存账号信息 [client]


服务管理
systemctl enable mysql.service
systemctl status mysql.service // 检查MySQL服务状态
systemctl stop mysql.service // 停止服务
systemctl start mysql.service // 启动服务
/etc/init.d/mysql restart // 重启 mysql
/etc/init.d/mysql start
service mysql status
service mysql stop
mysqladmin shutdown // 停止

/etc/my.conf
[mysql]
skip-grant-tables # 8.0 失效
default-character-set=utf8 # 设置mysql客户端默认字符集
[mysqld]
skip-grant-tables # 8.0 可能有效 待实测
port=3506 # 设置端口
basedir=C:\Program Files\mysql-5.7.18-winx64 # 设置mysql的安装目录
datadir=/var/lib/mysql # 设置mysql数据库的数据的存放目录
max_connections=200 # 允许最大连接数
character-set-server=utf8 # 服务端使用的字符集默认为8比特编码的latin1字符集
default-storage-engine=INNODB # 创建新表时将使用的默认存储引擎
socket=/var/lib/mysql/mysql.sock
user=mysql
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
 
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```

## 命令行

```
mysql
mysql -u root -p 登录
mysqld (-nt) -skip-grant-tables // 8.0 失效
mysqld --console --skip-grant-tables --shared-memory // 未起作用

mysqld
sudo mysqld --upgrade=FORCE // 用mysqld对MySql的一些文件进行升级

show
show global variables like 'port' // 查看端口
show databases;
show tables;
show tables from mysql;

use
use <table>

quit # 退出数据库
```

## 内置数据库

```
mysql
user 用户表
查看表信息
select host,user,plugin,authentication_string from mysql.user;

更改root用户的密码
update mysql.user set authentication_string=password('rootroot') where user='root'; // 8.0 password 函数失效 使用sha1代替
update user set authentication_string='' where  user = 'root';
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'yourpassword';
flush privileges; // 刷新数据库

新增用户
create user 'admin'@'%' identified by '123';
grant all on * to 'admin'@'%' with grant option;
alter user 'admin'@'%' identified with mysql_native_password by '456';

```

# Navicat

```
Navicat for MySQL_11.2.15
```











