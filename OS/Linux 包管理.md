> Thinking

```
apt # 管理 deb 包 (Debian Ubuntu)
	list # 
		--upgradable # 
	edit-sources # 

apt-get # 
apt-get update 更新本地包数据库列表
apt-get upgrade 仅升级已安装的软件包
apt-get dist-upgrade 可添加或删除程序包，以满足新的依赖
apt-get install 包名
apt-get install 包1 包2 … 安装所有列出的包
apt-get install -y 包名 无需提示直接安装
apt-get install -y gdebi&& sudo gdebi 包名.deb 使用gdebi检索缺少的依赖关系
apt-get remove 包名
apt-get autoremove 自动移除已知不需要的包

apt-cache
apt-cache search 搜索内容
apt-cache show 包名 显示有关软件包的本地缓存信息

apt-config

aptitude

dpkg # Debian Package
dpkg -s 包名 显示包的当前安装状态
dpkg -i 包名.deb 从本地文件系统直接安装包

yum # 管理 rpm 包(CentOS)
yum search 搜索内容
yum check-update 更新本地包数据库列表
yum update 升级软件包
yum search all 搜索内容 搜索所有内容，包括包描述
yum info 包名
yum deplist 包名 列出包的依赖
yum install 包名
yum install 包1 包2 … 安装所有列出的包
yum install -y 包名 无需提示直接安装
yum install 包名.rpm 从本地文件系统直接安装包
yum remove 包名 移除已安装的包

dnf # (Fedora)
dnf check-update 更新本地包数据库列表
dnf upgrade 升级软件包
dnf search 搜索内容
dnf search all 搜索内容 搜索所有内容，包括包描述
dnf info 包名
dnf repoquery –requires 包名 列出包的依赖
dnf install 包名
dnf install 包1 包2 … 安装所有列出的包
dnf install -y 包名 无需提示直接安装
dnf install 包名.rpm 从本地文件系统直接安装包
dnf erase 包名 移除已安装的包
```

> Memory

```

```

