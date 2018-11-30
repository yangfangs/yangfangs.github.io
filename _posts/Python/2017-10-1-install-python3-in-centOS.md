---
layout: post
title: CentOS 中安装 Python3
categories: Python
description: 安装 python3 centOS
keywords: centOS, install, Python3
---

　　由于 CentOS 默认使用的是 Python2, 并且默认的 yum 官方源不提供 Python3　的镜像，所以只有自己动手安装了。

# 安装必须的依赖

* 首先在管理员权限下安装好所有的依赖,不然会出现各种各样的报错和问题。

```bash
yum -y install zlib-devel bzip2-devel libffi-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make

```

# 获取 Python3 的最新安装包

* 这里获取的是当前最新的稳定版本 `3.7.1` 可以在 [Python官网](https://www.python.org/)获取最新发布版本。

```bash

wget "https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tar.xz"

```

# 解压和安装

* 解压

```bash

xz -d Python-3.7.1.tar.xz
tar xf Python-3.7.1.tar -C /usr/local/src/
cd /usr/local/src/Python-3.7.1/

```

* 安装

```bash
./configure --prefix=/opt/python3
make all
make install
make clean
```

# 查看安装好的 Python3 版本信息

```bash
/pot/python3/bin/python3 -V

```

# 软链接到当先用户

```bash
ln -s　/opt/python3/bin/python3 /usr/bin/python3

```

# 脚本使用python3

* 在 Python 脚本前加入注释行

```bash
#! /usr/bin/env python3

```



# 参考

* [CentOs6 安装PYTHON3](http://blog.csdn.net/hot_vc/article/details/48265835)
* [centos 6.5安装python3.4](http://blog.csdn.net/wang1144/article/details/52411373)

