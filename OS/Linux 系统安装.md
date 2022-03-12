> Thinking

```
发行版
环境变量
配置hosts
修改启动等待时间
搜过输入法
刷新 DNS 缓存
安装微信
```

> Memory

```
发行版
    Ubuntu
    Debian
    Fedora
    CentOS
环境变量
    /etc/profile
    $BASH_VERSION
    $PATH
    $HOME
    $JAVA_HOME
    $LANG
配置hosts
/etc/hosts hosts文件
151.101.76.133 desktop.githubusercontent.com
修改启动等待时间 /boot/grub/grub.cfg

搜过输入法
Fcitx 输入框架: fcitx
系统设置 -> 区域和语言 -> 管理已安装的语言 -> 语言tab -> 添加或删除语言-> 勾选中文（简体）
系统设置 -> 区域和语言 -> 管理已安装的语言 -> 语言tab -> 键盘输入法系统 -> fcitx
系统设置 -> 区域和语言 -> 管理已安装的语言 -> 语言tab -> 应用到整个系统

sudo dpkg -i sogoupinyin_版本号_amd64.deb // 安装本地deb包
sudo apt -f install // 解决依赖
sudo apt --fix-broken install
注销计算机重新登录

ctrl+space 切换输入法
shift 中英文切换

刷新 DNS 缓存
sudo killall -HUP mDNSResponder

安装微信
Snap安装包 完全独立于系统单独运行
sudo apt install snapd snapd-xdg-open
https://github.com/geeeeeeeeek/electronic-wechat/releases
sudo snap install electronic-chat
sudo snao remove electronic-wechat
electronic-chat



```

