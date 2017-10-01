---
layout: wiki
title: Linux会用到命令积累
categories: linux
description: linux　命令
keywords: linux, fedora
---

Linux 下常用命令积累

# Linux 发行版本查看

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

* 无论哪种方法都要带个`-h`转换成人类可读的模式(K,MB,GB等)。


# 升级Fedora发行版本的方法

* 以Fedora 24升级到 Fedora 25为例:

```bash
dnf install dnf-plugin-system-upgrade
dnf system-upgrade download --releasever=25
# 重启
dnf system-upgrade reboot
```

# Fedora下安装Rstudio的方法

* 主要是使用`rpm`命令来安装(需要下载rpm格式的安装包)，如下：

```bash
$ wget "wget http://download2.rstudio.org/rstudio-1.0.136-x86_64.rpm"
$ rpm -Uvh rstudio-1.0.136-x86_64.rpm"

```

# Linux　下常用的解压和压缩命令

* 明白几个常用的参数意思：

| 参数  |  解释   |
| ----- |-----|
| -c | create的缩写，所以在创建压缩文档时候使用  |
| -x | extract的缩写，所以在解压时候使用        |
| -t | list的缩写，所以在查看压缩文档时候使用    |
| -v | verbose的缩写，即详细列出处理文件的过程，一般都会带上，不建议后台运行  |
| -v | verbose的缩写，即详细列出处理文件的过程，一般都会带上，不建议后台运行  |
| -z | 使用gzip 压缩  |
| -j | 使用bzip2 压缩  |

## 只是打包不压缩

* 解包：

```bash
tar xvf FileName.tar
```

* 打包：

```bash
tar cvf FileName.tar DirName
```

## 只是压缩(.gz)为例

* 解压：

```bash
gunzip FileName.gz

# 或
gzip -d FileName.gz
```

* 压缩：

```bash
gzip FileName
```

## 同时打包和压缩

### `.gz` 格式

* 解压

```bash
tar zxvf FileName.tar.gz
```

* 压缩

```bash
tar zcvf FileName.tar.gz DirName

```

### `.bz2` 格式

* 解压

```bash
tar jxvf FileName.tar.bz2
```

* 压缩

```bash
tar jcvf FileName.tar.bz2 DirName
```

## '.zip'　格式

* 解压

```bash
unzip FileName.zip
```

* 压缩

```bash
zip FileName.zip DirName
```



***

**2017-4-12更新**

***