---
layout: post
title: Python 参数解析Parser的使用方法
categories: Python
description: Parser的使用方法
keywords: command line, python, parser
---

# 基本用法

* 创建一个argparse的对象来操作

```python
import argparse #导入
parser = argparse.ArgumentParser()　#创建实例对象
parser.parse_args()　# 解析
```

# 添加参数

## 位置参数

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("echo")　# 添加参数
args = parser.parse_args()
print args.echo

```


## 可选参数

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--verbosity", help="increase output verbosity")
args = parser.parse_args()
if args.verbosity:
    print "verbosity turned on"
```

# 一个模板

```python
    parser = argparse.ArgumentParser()
    parser.add_argument('-m', '--msg_p', action='store', dest="msg_path",
                        help="path")
    parser.add_argument('-g', action='store', dest="graph",
                        help="input graph")
    parser.add_argument('-p', action='store', dest="prizes",
                        help="input prizes")
    parser.add_argument('-t', action='store', dest="terminals", default=None,
                        help="input terminals")
    parser.add_argument('-o', action='store', dest="output", default='pcsf.graphml',
                        help="graphML format to cytoscape")
    args = parser.parse_args()
```

## 参考:

* [Argparse Tutorial](https://docs.python.org/2/howto/argparse.html)
