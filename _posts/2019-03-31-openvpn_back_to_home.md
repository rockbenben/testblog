---
layout:       post
title:        "OpenVPN 随时随地回家的路"
subtitle:     ""
date:         2019-03-31
author:       "Benson"
header-img:   img/post-bg-20180108.jpg
header-mask:  0.3
catalog:      true
categories:
    - 网络
tags:
    - OpenVPN
    - 内网穿透
---
有时在外面需要访问家里的文件，或直接利用家中网络设置翻墙。为此，利用路由器 OpenVPN 搭建了一条回家的路。

## 内网穿透

连接家中内网，家里必须有个固定的访问地址。我将子域名 home.xxx.com 指向家中 IP。

梅林路由器进入「高级设置」→「外部网络（WAN）」→「DDNS」，将路由器指向准备好的子域名。

![](http://tc.seoipo.com/20190331203233.png)

电信分配的公网 IP 经常会更换，每次都需要重定向子域名。在路由器 koolshare - 软件中心中安装 Aliddns，帮助更新家的公网 IP。插件中输入定向子域名和阿里云的 appkey，配置就完成了。如果没有自动在阿里云解析，可以先手动解析设置。

光猫设置参考 [光猫改造 篇三：百卓 GP1700 进阶设置 - 端口映射](https://newzone.top/p/2018-06-08-Baizhuo_GP1700/)。

## OpenVPN 配置

内网穿透完成后，开始 OpenVPN 配置。梅林路由器进入「高级设置」→「VPN」→「虚拟专用网（VPN）服务器」，开启路由器自带的 OpenVPN。

![](http://tc.seoipo.com/20190331200921.png)

高级配置红色的部分有修改，特别是**VPN 子网必须修改为与路由器不同的号段**，如 192.168.3.0。如果使用默认子网，会无法顺利翻墙。

应用设置后，点击「一般设置」，并导出 .ovpn 文件。打开该配置文件，将远程端口改为光猫上虚拟服务器映射的端口。

![](http://tc.seoipo.com/20190331202017.png)

最后，手机导入`.ovpn`设置文件，就可以上网回家了！