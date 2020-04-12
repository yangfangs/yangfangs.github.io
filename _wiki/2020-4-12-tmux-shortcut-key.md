---
layout: wiki
title: Tmux 常用快捷键
categories: linux
description: linux　命令, tumx 快捷键
keywords: linux, tmux,
---

Tmux 是服务器端取代传统 Terminal 的神器，分屏幕操作，多任务操作，后台运行（取代 nohup 命令 ），任务恢复
（再次链接服务器恢复上次断开时候的Terminal的环境，继续工作），总结下tmux使用方法和快捷键，方便查询。

# 安装 Tmux (centOS 环境)

```bash
$ yum -y install tmux
```

# 常用命令

## 终端中使用tmux命令

* 启动 tmux 使用 `-s` 命令指定会话名称，使用 `-n` 命令指定窗口名称

```bash
$ tmux new -s sessionName -n window
```

* 退出会话(tmux会话内命令)

```bash
$ tmux detach
```

* 退出并关闭会话（窗口,窗格）

```bash
$ exit
```
* 结束后台的会话

```bash

#通过会话编号

$ tmux kill-session -t 0

#通过会话名称

$ tmux kill-session -t sessionName 

```

* 查看所有会话
```bash
$ tmux ls
```

* 激活会话

```bash
$ tmux attach -t sessionName
```



## tmux 内使用前缀 Ctrl+b 然后对应快捷键执行命令

### 会话常用快捷操作

|  快捷键 | 说明     |
|--------|---------|
|  ? | 所有快捷键，q退出  |
|  :new sessionName | 创建新会话  |
| s  |  切换会话 |
| $  |  重命名当前会话 |
| d  | 离开会话返回shell（与tmux detach功能相同）|
| Ctrl+z| 挂起会话，返回shell |

### 窗口常用快捷操作

|  快捷键 | 说明     |
|--------|---------|
| c | 创建新窗口  |
| w  | 显示窗口 |
| 数字键  | 选择对应窗口 |
| p  | 前一个窗口  |
| n  | 后一个窗口  |
| f  | 查找窗口  |
| ,  | 重命名窗口  |
| &  | 关闭窗口（带提示）  |

### 窗格常用快捷键

|  快捷键 | 说明     |
|--------|---------|
| %  | 垂直分割  |
| "  | 水平分割 |
| o  | 切换窗格  |
| x  | 关闭窗格  |
| space  | 切换窗格布局  |
| q  | 显示窗格编号，按对应数字选择窗格  |
| {  | 与上一个窗格调换位置  |
| }  | 与下一个窗格调换位置  |
| z  | 当前窗格最大化  |
| !  | 取消所有窗口保留当前窗口  |
| Ctrl+方向键  | 以1个单元格为单位移动边缘以调整当前窗格大小 |
| Alt+方向键  | 以5个单元格为单位移动边缘以调整当前窗格大小 |