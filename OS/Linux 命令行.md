> Thinking

```
rm # 删除文件
	-rf # 

cd # 
cd .
cd ..

ls

mv

del

rd

mkdir

tar
tar xvf mysql-server_8.0.12-1ubuntu18.04_amd64.deb-bundle.tar
tar -zxvf <file>

history
history -c

ifconfig

echo
echo $PATH

cp
sudo cp /boot/grub/grub.cfg /boot/grub/grub.cfg.bak

ln # 建立软连接 快捷方式
ln -s /usr/bin/python3.5 /usr/bin/python

grep
ls -l | grep python

bash
ctrl + c 取消当前指令

clear

who
who -b 查看最后一次系统启动时间
who -r 查看当前系统运行时间

last
last reboot Linux系统历史启动时间
last reboot | head -1 查看最后一次Linux系统启动的时间

top
up 后表示系统到目前运行了多长时间

w
up后表示系统到目前运行了多久时间

uptime
up后表示系统到目前运行了多久时间

wget
wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb

chmod 777 <file> 修改权限

snap
sudo apt install snap
sudo apt install snapd snapd-xdg-open
sudo snap install electronic-wechat
snap changes
sudo snap abort 12
sudo apt-get install libcanberra-gtk-module

/proc/uptime
cat /proc/uptime
date -d "`cut -f1 -d. /proc/uptime` seconds ago"
date -d "$(awk -F. '{print $1}' /proc/uptime) second ago" +"%Y-%m-%d %H:%M:%S"

```

> Memory

```
Ctrl + R
services.msc // 服务



```

