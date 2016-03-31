---
layout: post
title: Linux 下设置环境变量
categories: Linux
description: 环境变量
keywords: setpath, Linux
---

  设置环境变量,就是来告诉 Shell 到哪里去找你要执行的命令,例如执行 pwd 命令,就能显示当前工作目录,其实 Shell 在执行这个命令时候是在 `/usr/bin/pwd` 下寻找这个可执行命令的。若想在任何地方执行一个可执行文件,而不想在前面加上长长的绝对路径,就需要自己来设置环境变量了。


### 1.直接导入 `export`

```bash
export PATH=$PATH:/home/fedora/example

```
* 这样就把路径 `/home/fedora/example` 导入到了系统变量中了

### 2.在 `profile` 文件最后加入环境变量

* 打开 `profile` 编辑

```bash
vim /etc/profile

```

* 在最后面加入环境变量

```bash
export PATH="$PATH:/home/fedora/example"

```
* 重启生效或 `bash` 中执行下面语句生效

```bash
source /etc/profile

```

### 3.修改 home 目录下 `.bash_profile` 文件 

* 打开 `bash_profile` 编辑

```bash
vim ~/.bash_profile

```

* 在最后面加入环境变量

```bash
export PATH="$PATH:/home/fedora/example"

```
* 重启生效或 `bash` 中执行下面语句生效

```bash
source ~/.bash_profile

```

### 4.修改 .bashrc 文件


* 打开 ` .bashrc` 编辑

```bash
vim ~/.bashrc

```

* 在最后面加入环境变量

```bash
export PATH="$PATH:/home/fedora/example"

```
* 重启生效或 `bash` 中执行下面语句生效

```bash
source ~/.bashrc

```

#### 注意

* 方法 1 是临时的修改,关闭终端失效
* 方法 2 修改系统级别的环境变量
* 方法 3 修改用户级别的环境变量
* 方法 4 修改用户级别的环境变量
* 查看当前环境变量使用

```
echo $PAHT

```