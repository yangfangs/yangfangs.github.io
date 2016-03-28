---
layout: post
title: Fedora下安装PyCharm-Community版本
categories: Python
description: 安装PyCharm
keywords: PyCharm,install
---

　　在 Fedora 下安装一个非常强大的 Python IDE------->PyCharm-Community版本,有一个非常方面的方法,三步就可以安装上。记录一下方便以后再装

### 在源文件中添加pycharm.repo,

* 以 root 权限再终端运行
* ` vim /etc/yum.repos.d/pycharm.repo`

### 添加以下内容到源中

```bash
[phracek-PyCharm]
name=Copr repo for PyCharm owned by phracek
baseurl=https://copr-be.cloud.fedoraproject.org/results/phracek/PyCharm/fedora-$releasever-$basearch/
skip_if_unavailable=True
gpgcheck=1
gpgkey=https://copr-be.cloud.fedoraproject.org/results/phracek/PyCharm/pubkey.gpg
enabled=1
enabled_metadata=1
```

### 然后安装

* dnf copr enable phracek/PyCharm
* dnf install pycharm-community


### 参考资料

* [technical blogs & poems](http://www.leeladharan.com/installing-pycharm-community-on-32-or-64-bit-fedora-21-22-23)
