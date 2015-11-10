---
layout: post
title: Markdown简明语法
category: Java
tags: Linux下java环境搭建
keywords:
description:
---

#Ubuntu 下快速配置java环境的方法

##你必须知道的JRE、 OpenJDK 、JDK
* JRE(Java Runtime Environment),是你运行java程序的必须环境,没有这个环境的话你的java程序是无法运行的.
* JDK(Java Development Kit),是你开发java程序的必须工具,没有这个工具你是无法进行java开发的.
* OpenJDK是java开发的开源实现,是一个开源的工具,当然你也可以选择 Oracle JKD的java开发工具包(官方).

##测试java是否已经安装
* 打开终端,输入命令:
* java -version
* 如果有java版本信息就已经安装,若没有就需要我们安装

##以下方法直接通过ppa安装Oracle JDk
* 打开终端输入:
* sudo add-apt-repository ppa:webupd8team/java
* sudo apt-get update
* sudo apt-get install oracle-java8-installer
* sudo apt-get install oracle-java8-set-default
* 上面方法需要下载Oracle官方JDK(150MB左右),根据你的网路速度需要等待时间不同
* 以上方法的好处是装上就能开发了,不需要手动配置环境变量

##配置Eclipse
* 首先到[Eclipse官网](http://www.eclipse.org/downloads/?osType=linux&release=undefined)下载最先的eclipse,现在eclipse官网提供了更为方便的安装方法,提供一个eclipse安装器--Eclipse installer,下载Linux版本到本地.
* 解压tar -zxvf eclipse-inst-linux64.tar.gz,得到文件eclipse-installer
* cd eclipse-installer 
* ./eclipse-inst
* 选择你需要的版本,我就选的第一个,进行java开发用的
* 然后自动安装本地,打开就可以使用了

##配置终端打开eclipse
* cd /usr/local/bin
* sudo ln -s /home/yangfang/eclipse/eclipse #-s后面是你eclipse位置
* 打开终端输入eclipse打开eclipse搞定了

##加入eclipse到unbuntu托盘
* cd /usr/share/applications
* sudo gedit eclipse.desktop
* 在文件中写入以下代码,其中Exec后面是你安装eclipse启动的路径,Icon是你eclipse的图标路径,这里需要替换你自己安装eclipse路径

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
* 然后就可以在托盘中发现eclipse图标,然后拖动到桌面就行了