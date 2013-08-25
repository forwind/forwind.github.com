---
layout: post
title: "树莓派无线上网配置"
description: ""
category: raspberrypi
tags: [raspberrypi]
---

关于树莓派的一个小总结。有玩的朋友，欢迎留言联系我。//for_wind

## 购买和配置 ##

#### 树莓派 ####

- 型号：RASPBERRY-PI RASPBRRY-MODB-512M

- 商家： e络盟  

- 价钱：

	物品小计：CNY 235.00

	基本运输：CNY 30.00

	增值税：CNY 45.05

	总计：CNY 310.05

	备注：我买的时候，貌似512M版本刚刚出来。是UK版。据说后来的中国产的有很多问题，具体不详。

![树莓派]({{ site.img_url }}/rpi1.jpg)
#### 无线网卡：####
型号：Fast 迅捷 FW150US 超小型150M无线USB网卡

商家和价钱：淘宝上面买的。当时总价23元（6元运费）

备注：这个是树莓派爱好者论坛上推荐的型号。大家也可以试试其它的。

####内存卡：####
型号：Transcend 创见 SDHC Class10 16G SD卡

商家和价钱：亚马逊，当时60
####电源：####
型号：HTC手机电源线

##系统 ##
Raspbian “wheezy”：


> If you’re just starting out, this is the image we recommend you use. It’s a reference root filesystem from Alex and Dom, based on the Raspbian optimised version of Debian, and containing LXDE, Midori, development tools and example source code for multimedia functions.

下载地址：[树莓派官网](http://www.raspberrypi.org/downloads)

## 现在开始  ##
 
全部配置的清单在上面第1部分。完成第2步后，让我们开始树莓派之旅。

所用软件有：PuTTY，VNC。

参考资料：

A、[SSH远程管理树莓派（一）基本教程：使用PuTTY登录到树莓派](http://bbs.shumeipai.org/thread-53-1-1.html)
B、[VNC远程登录树莓派的图形界面（桌面环境）[一帖完结]](http://bbs.shumeipai.org/thread-113-1-1.html)

感谢shamiao的帮助。（额，问那些白痴问题的，是我for_wind童鞋）

**总结步骤如下：**

**①插入内存卡，连上电源，同时将网线和无线网卡连上树莓派**

无显示器操作，是不能一开始就用无线网卡的。 需要先临时插上有线网，通过有线网络连接派，去配置无线网络。 配置好无线网之后，就可以把网线拔掉，只接无线网卡了。

**②扫描IP地址，获取树莓派分配到的IP地址**
可以使用[Advanced IP Scanner](http://bbs.shumeipai.org/thread-108-1-1.html)（稍等一会儿，扫描需要一点时间）

或者直接192.168.1.1

获取了树莓派的IP地址和MAC地址后，建议通过DHCP服务器->静态地址分配，将树莓派的IP地址固定，免去以后的第②步。

**③SSH连接树莓派，输入sudo raspi-config做首次开机设置，然后按教程安装VNC。**

通过VNC可以登录到树莓派的桌面环境，而[通过SSH可以操作树莓派的命令行](http://bbs.shumeipai.org/thread-53-1-1.html)。（点击按照教程来即可）

为何*SSH*？

> SSH 为 Secure Shell 的缩写，由 IETF 的网络工作小组（Network Working Group）所制定；SSH 为建立在应用层和传输层基础上的安全协议。SSH 是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。

**④VNC连接树莓派的桌面环境，桌面上有一个Wi-Fi Config工具，使用那个连接无线网。**

基本上安装教程即可。注意安装VNC服务器设置好开机自动启动后，重启一下树莓派。如果连接不上，可以多试连几次，可能机器还没有反应过来，额。我猜。

![启动VNC]({{ site.img_url }}/rpi2.jpg)

![输入密码raspberrypi]({{ site.img_url }}/rpi3.jpg)

![系统界面]({{ site.img_url }}/rpi4.jpg)


**⑤连接好无线网，再去扫描IP，就能同时扫到有线/无线的两个IP地址了。**

现在输入无线网络的ssid和密码psk。接着通过命令行输入ifconfig，可以查看到wlan0（wifi）的ip。
![系统界面]({{ site.img_url }}/rpi5.jpg)

⑥拔掉网线。今后就使用无线网卡的IP地址连接即可。

（即在上一步中提到的IP地址）用Wi-Fi Config工具连接的无线网络，每次开机都会自动连接。所以此时就可以仅用无线网卡了。

需要说明的是，在有网线的时候，树莓派的五盏灯（ACT，PWR，FDX，LNK，100）都在亮。等拔掉网线后，只有两盏亮（ACT，PWR）。

而且需要注意的是，VNC-Viewer第一次使用本地网线（eth0）连线后的IP地址，而在拔掉网线后，VNC-Viewer连接失败，重启后，应使用无线网卡wlan0中显示的IP地址。两者有所不同。

参考网址：

树莓派爱好者论坛：[http://bbs.shumeipai.org/forum.php](http://bbs.shumeipai.org/forum.php)

{% include JB/setup %}
