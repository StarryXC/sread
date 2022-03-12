> Thinking

```
Android 源码目录结构

https://source.android.google.cn/
AndroidXRef就是其中一款备受青睐的源码在线阅读网站【网址：http://androidxref.com/】
需要VPN，即需要FQ
Android SDK Search 使用方法】
```

> Memory

```
sudo apt-get install git git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev libc6-dev 
sudo apt-get install lib32ncurses5-dev x11proto-core-dev libx11-dev 
sudo apt-get install lib32z-dev libgl1-mesa-dev g++-multilib mingw32 tofrodos python-markdown 
sudo apt-get install libxml2-utils xsltproc gcc-multilib lib32readline5-dev
sudo apt-get install git

编译
source build/envsetup.sh
编译安卓源码
make (也可以使用 make -j4 四线程编译)
运行模拟器
lunch sdk-eng
emulator
emulator -kernel ./kernel/goldfish-android-goldfish-3.4/arch/arm/boot/zImage 指定内核启动模拟器
编译SDK
make -j4 sdk

命令查看内核版本
adb shell
cd proc
cat version

source build/envsetup.sh
mmm development/tools/idegen/ 编译idegen模块 mmm命令会把system.img等文件删除
out/host/linux-x86/frameworks/目录下生成了idegen.jar文件

development/tools/idegen/idegen.sh 根目录下生成
android.iml和android.ipr这两个文件，这两个文件是Android Studio的工程配置文件
make snod 重新生成镜像

源码地址 Android社区
https://www.androidos.net.cn/sourcecode
https://www.androidos.net.cn/android/9.0.0_r8/tree


```

