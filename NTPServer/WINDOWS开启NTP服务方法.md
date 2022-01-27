# WINDOWS开启NTP服务方法

方法详见：[windows搭建NTP时钟服务器（win xp、7、8、10）](https://jingyan.baidu.com/article/b0b63dbf5d84334a483070fa.html)

注意：1，NTP服务使用UDP协议123端口，需要建立防火墙入站规则

​			2，需要开启 设置-时间和语言-日期和时间-自动设置时间 选项

## 1、运行regedit，打开系统注册表

进入注册表项 HKEY_LOCAL_MACHINE—>SYSTEM—>CurrentControlSet—>Services—>W32Time—>TimeProviders—>NtpServer  Enabled 设置为 1 打开NTP（系统默认0）；

进入注册表项 HKEY_LOCAL_MACHINE—>SYSTEM—>CurrentControlSet—>Services—>W32Time—>Config 

AnnounceFlags 设置为 5 （系统默认 10）；

## 2、运行services.msc，打开系统服务

第一、将Windows time服务设置为自动启动，点击应用和确定；

第二、鼠标右键重新启动windows time服务；

## 3、重新启动电脑

重新启动电脑或者主机，所有配置生效，NTP时钟搭建完毕，此时只需其他设备将本电脑IP填入时钟同步，点击更新即可同步改时钟。

