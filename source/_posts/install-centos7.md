---
title: 用VirtualBox虚拟机安装CentOS7系统
date: 2016-06-29 10:37:42
categories: 教程
tags: [系统,虚拟机]
---

>介绍
>CentOS（Community Enterprise Operating System）是Linux发布版之一，它是来自于Red Hat Enterprise Linux依照开放源代码规定发布的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以CentOS替代商业版的Red Hat Enterprise Linux使用。两者的不同，在于CentOS并不包含封闭源代码软件。CentOS 对上游代码的主要修改是为了移除不能自由使用的商标。2014年，CentOS宣布与Red Hat合作，但CentOS将会在新的委员会下继续运作，并不受RHEL的影响，CentOS 和 RHEL 一样，都可以使用 Fedora EPEL 来补足软件。


>VirtualBox 是一款开源虚拟机软件，由德国InnoTek软件公司出品。现在则由甲骨文公司进行开发，是甲骨文公司xVM虚拟化平台技术的一部份。它提供用户在32位或64位的Windows、Solaris及Linux 操作系统上虚拟其它x86的操作系统。用户可以在VirtualBox上安装并且运行Solaris、Windows、DOS、Linux、OS/2 Warp、OpenBSD及FreeBSD等系统作为客户端操作系统。
><!--more-->

# 安装

### 首先得准备以下两样东西

* VirtualBox([下载地址](https://www.virtualbox.org/wiki/Downloads))
* CentOS 7镜像文件([下载地址](http://mirrors.cug.edu.cn/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1511.iso))


### 新建虚拟机

打开已经安装好的VirtualBox
![](/images/install-centos7/centos7_install_1.jpg)
名称随意，一般取系统名字，这里用CentOS 7,类型选Linux，版本选图中所示，如果选项中没有64位的，[可以参考这里](http://blog.csdn.net/yongf2014/article/details/49282333)

继续，内存大小设置为678MB左右就满足以图形化界面安装系统了，如果太低，就进不了，这就是为什么有些人安装的时候老是说我怎么进不了图形化界面的原因
![](/images/install-centos7/centos7_install_2.jpg)
下一步
![](/images/install-centos7/centos7_install_3.jpg)
创建
![](/images/install-centos7/centos7_install_4.jpg)
下一步
![](/images/install-centos7/centos7_install_5.jpg)
下一步
![](/images/install-centos7/centos7_install_6.jpg)
虚拟硬盘选择10GB，至于这些配置项的意义，大家可以自己去研究，这里不再阐述了

  

### 设置系统属性

点开VirtualBox左上角的设置，系统设置，把光驱设为第一个启动
![](/images/install-centos7/centos7_install_7.jpg)

存储设置，点击属性那栏右边那个光盘小图标，选择下载好的镜像文件

![](/images/install-centos7/install-centos7/centos7_install_8.jpg)

网络，桥接网卡，指定你的本地连接那块网卡

![](/images/install-centos7/centos7_install_9.jpg)

启动VirtualBox左侧的CentOS 7，选择第一个Install CentOS 7，开始安装
![](/images/install-centos7/centos7_install_10.jpg)

设置语言

![](/images/install-centos7/centos7_install_11.jpg)

点击软件选择

![](/images/install-centos7/centos7_install_12.jpg)


选择安装GNOME桌面版

![](/images/install-centos7/centos7_install_13.jpg)

点击安装位置
![](/images/install-centos7/centos7_install_14.jpg)


选择自动分区，点击完成
![](/images/install-centos7/centos7_install_15.jpg)

点击网络和主机名

![](/images/install-centos7/centos7_install_16.jpg)

如图所示，可用时自动链接到这个网络，打钩

![](/images/install-centos7/centos7_install_17.jpg)

按顺序配置好你的网络

![](/images/install-centos7/centos7_install_18.jpg)

点击开启，完成

![](/images/install-centos7/centos7_install_19.jpg)
​	
### 开始安装

![](/images/install-centos7/centos7_install_20.jpg)

设置好root密码和一个普通用户

![](/images/install-centos7/centos7_install_21.jpg)

安装完成，要求你重启

![](/images/install-centos7/centos7_install_22.jpg)


点击下面黄色的许可协议，进去之后同意


![](/images/install-centos7/centos7_install_24.jpg)

不启用Kdump，提示你重启

![](/images/install-centos7/centos7_install_25.jpg)

系统安装完成

![](/images/install-centos7/centos7_install_26.jpg)
​	
​	
​	
​	
​	
本文内容转载自[闲来无事](http://www.aiplaypc.com/102.html)
​	

​	

  