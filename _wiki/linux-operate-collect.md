---
layout: wiki
title: Linux会用到命令积累
categories: linux
description: linux　命令
keywords: linux, fedora
---

Linux 下常用命令积累

# linux 发行版本查看

* 查看发行版本

```bash
$ lsb_relase -a
```
适用于Linux所以发行版本，Ubuntu，Fedora，Centos等

* 查看内核版本

```bash
$ uname -a
#或者
$ uname -r
```
适用于Linux所以的发行版， Ubuntu，Fedora，CentOS等

# 查看目录中所有文件大小

* 1.使用 `ls -lht` 或　`ll -ht`

```
$ ls -lht
total 28K
-rw-rw-r-- 1 yangfang yangfang   28 Dec 26 16:08 file.txt
-rwxrwxr-x 1 yangfang yangfang 8.0K Dec 18 20:00 libtest.so
-rw-rw-r-- 1 yangfang yangfang 1.6K Dec 18 20:00 libtest.o
-rw-rw-r-- 1 yangfang yangfang  147 Dec 18 20:00 libtest.c
-rw-rw-r-- 1 yangfang yangfang 1.3K Nov  8 19:54 test.txt
-rw-rw-r-- 1 yangfang yangfang 1.3K Nov  8 19:54 test.py
```

* 2.也可以使用`du -sh *`

```
$ du -sh *
4.0K    file.txt
4.0K    libtest.c
4.0K    libtest.o
8.0K    libtest.so
4.0K    test.py
4.0K    test.txt
```

* 无论哪种方法都要带个'-h'转换成人类可读的模式(K,MB,GB等)。




***

**2016-12-26更新**

***