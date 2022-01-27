# ADB基本用法

使用ADB前，安卓设备要开启“开发者选项-调试-USB调试”或者“开发者选项-调试-网络调试”
使用方法：https://blog.csdn.net/qq_33003441/article/details/80973744
                https://www.e-learn.cn/content/qita/1057990

查看adb版本：	adb version
查看连接列表：	adb devices
网口连接：	adb connect 192.168.6.96:5566
控制远端：	adb shell xxx
重启远端：	adb reboot

# 问题1：ADB版本不一致

提示：adb server version (31) doesn't match this client (41); killing...

说明：目标机的adb版本为31，而本地adb版本为41

解决：将目标机的adb版本与本地adb版本一致

例子：目标机为模拟器，将本地的adb3文件覆盖模拟器目录下的adb3文件

adb3文件：adb.exe AdbWinApi.dll AdbWinUsbApi.dll

# 问题2：ADB服务端口5037被占用

在命令行中 输入以下命令，查询占用5037端口的应用的PID

~~~cmd
netstat -ano|findstr “5037” 
~~~

在使用以下命令，查看PID对应的程序（PID为15828），关闭对应的程序，再运行目标机

~~~cmd
tasklist |findstr “15828”
~~~

