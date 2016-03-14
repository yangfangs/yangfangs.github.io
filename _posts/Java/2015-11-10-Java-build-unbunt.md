---
layout: post
title: Java开发环境搭建(ubuntu)
categories: Java
description:
keywords: Java,Ubuntu,环境配置
---

# Ubuntu 下快速配置java环境的方法

## 你必须知道的 JRE、 OpenJDK 、JDK

* JRE(Java Runtime Environment) ,是你运行 java 程序的必须环境,没有这个环境的话你的 java 程序是无法运行的.
* JDK(Java Development Kit) ,是你开发 java 程序的必须工具,没有这个工具你是无法进行 java 开发的.
* OpenJDK是 java 开发的开源实现,是一个开源的工具,当然你也可以选择 Oracle JKD 的 java 开发工具包(官方).

## 测试 java 是否已经安装

* 打开终端,输入命令:
* java -version
* 如果有 java 版本信息就已经安装,若没有就需要我们安装

## 以下方法直接通过 ppa 安装 Oracle JDk

* 打开终端输入:
* sudo add-apt-repository ppa:webupd8team/java
* sudo apt-get update
* sudo apt-get install oracle-java8-installer
* sudo apt-get install oracle-java8-set-default
* 上面方法需要下载 Oracle 官方 JDK(150MB左右) ,根据你的网路速度需要等待时间不同
* 以上方法的好处是装上就能开发了,不需要手动配置环境变量

## 配置 Eclipse

* 首先到 [Eclipse官网](http://www.eclipse.org/downloads/?osType=linux&release=undefined) 下载最先的 eclipse ,现在 eclipse 官网提供了更为方便的安装方法,提供一个 eclipse 安装器 --Eclipse installer ,下载 Linux 版本到本地.
* 解压 tar -zxvf eclipse-inst-linux64.tar.gz ,得到文件 eclipse-installer
* cd eclipse-installer 
* ./eclipse-inst
* 选择你需要的版本,我就选的第一个,进行java开发用的
* 然后自动安装本地,打开就可以使用了

## 配置终端打开 eclipse

* cd /usr/local/bin
* sudo ln -s /home/yangfang/eclipse/eclipse #-s后面是你eclipse位置
* 打开终端输入 eclipse 打开 eclipse 搞定了

## 加入 eclipse 到 unbuntu 托盘

* cd /usr/share/applications
* sudo gedit eclipse.desktop
* 在文件中写入以下代码,其中 Exec 后面是你安装 eclipse 启动的路径, Icon 是你 eclipse 的图标路径,这里需要替换你自己安装 eclipse 路径

```
[Desktop Entry]
Type=Application
Name=eclipse
Comment=Java
Exec=/home/yangfang/eclipse/java-mars/eclipse/eclipse
Icon=/home/yangfang/eclipse/java-mars/eclipse/icon.xpm
Categories=Development
Terminal=false
```

* 然后就可以在托盘中发现 eclipse 图标,然后拖动到桌面就行了