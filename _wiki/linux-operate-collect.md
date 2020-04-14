---
layout: wiki
title: Linux 常用命令积累
categories: linux
description: linux　命令
keywords: linux, fedora
---

Linux 环境常用命令积累

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

### .gz 格式

* 解压

```bash
tar zxvf FileName.tar.gz
```

* 压缩

```bash
tar zcvf FileName.tar.gz DirName

```

### .bz2 格式

* 解压

```bash
tar jxvf FileName.tar.bz2
```

* 压缩

```bash
tar jcvf FileName.tar.bz2 DirName
```

### .zip　格式

* 解压

```bash
unzip FileName.zip
```

* 压缩

```bash
zip FileName.zip DirName
```


# Linux　命令行与服务器交互

## 登录服务器使用 ssh　命令

### 以 root　账户登录

```bash
ssh 192.168.1.100

```

### 以用户登录


```bash
ssh username@192.168.1.100

```

## 上传和下载 scp 命令

### 上传

* 上传文件：上传本地　`file.txt` 到远程服务器 `/home/work/` 目录下


```bash
scp /home/work/file.txt username@192.168.1.100:/home/work/

```

* 上传整个文件夹：上传整个 `dir`　目录到服务器　`/home/work/` 目录下

```bash
scp -r /home/work/dir username@192.168.1.100:/home/work/

```

### 下载

* 下载服务器文件 `file.txt`到本地　`/home/work/` 目录下

```bash

scp username@192.168.1.100:/home/work/file.txt /home/work/
```

* 下载服务器目录 `dir` 到本地 　`/home/work/` 目录下

```bash

scp -r username@192.168.1.100:/home/work/dir /home/work/
```


# nohup--断开链接服务器依然运行(后台)

* 本地链接上服务器跑程序时候，我们并不想在关闭 `terminal`　后程序就不运行了，而是想挂在服务器上让程序一直运行，直到结束。 `nohup`命令可以实现

```bash

nohup command

```

* 或者指定输出日志

```bash

nohup command > output.log

```
# 统计当前目录下的文件个数

* 统计目录下的文件个数(仅文件)

```bash
$ ls -l | grep "^-" | wc -l

```
* 统计目录下的目录个数(仅目录)

```bash
$ ls -l | grep "^d" | wc -l

```

**若要进行递归目录下的目录也统计的话，第一个管道前命令改为*$ ls -lR*即可**


# Linux下配置使用shadowsocks

1.安装shadowsocks

```bash

pip install shadowsocks

```


2.写入配置shadowsocks到json文件

* 文件名为`ss.json`

```python

{
"server":"11.16.266.108",
"server_port":2562,
"local_port":1080,
"password":"1234",
"timeout":600,
"method":"aes-256-cfb"
}

```
3.启动

```bash
sslocal -c ss.json
```

4.在终端中也使用代理上网(临时，关闭终端就无效了)

```bash
export ALL_PROXY=socks5://127.0.0.1:1080

```

# Linux下的软硬链接ln命令

* 软链接：相当于win下的快捷方式，删除源文件后链接失效
* 硬链接：相当于复制一份源文件，删除源文件后不影响链接

```bash

#ln实现硬链接
$ ln sourceFile NewFile

#ln -s 实现软链接
$ ln -s sourceFile NewFile

```

***

**2020-4-14更新**

***