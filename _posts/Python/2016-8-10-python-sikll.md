---
layout: post
title: Python 中的一些小技巧
categories: Python
description: Python skill
keywords: Development, Skill, Python
---

　　积累一些在使用Python中能用到的一些技巧！


# 生成一个独一无二的时间文件夹

```python
import time
timeformat = '%Y%m%d%H%M%S'
timeinfo = str(time.strftime(timeformat))
timeinfo
'20160810180815'
```

# 去除list中的空字符串

* 例如 `a = ['a','b','','c']`　去除其中的空字符串

```python
def removeEmptyString(inputlist):
    temp = []
    for line in inputlist:
        if line:
            temp.append(line)
    return temp
```

* 或者使用一行迭代, 更简洁, 速度更快

```python
b = [var for var in a if var]
print(b)
```


# 定位当前脚本的绝对路径

```python
import os
def getlocalpath():
    relpath = os.path.split(os.path.realpath(__file__))[0]
    return relpath
```

# 判断目录若不存在则创建

```python
import os
if not os.path.exists(dirname):
    os.makedirs(dirname)
```

# list 取交集，并集和差集

* 例如 `a = ['a','b','c']`，`b = ['b','c','d']`

* 交集:

```python
print list(set(a).intersection(set(b)))

#或者
isec = [val for val in a if val in b]
print isec

```

* 并集

```python
print list(set(a).union(set(b)))
```

* 差集

```python
print list(set(b).difference(set(a))) # b-a

```


# 把一个list分割成固定长度子list

例如　`list1 = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]` 分割成固定长度为3的子list

```python
def splite_list(splist, s):
    """splite a list to sub list contain s"""
    return [splist[i:i + s] for i in range(len(splist)) if i % s == 0]

#test
list1 = range(10)
splite_list(list1,2)
[[0, 1], [2, 3], [4, 5], [6, 7], [8, 9]]
```

# 在Python中调用Linux下的export

* Python中改变Linux 的环境变量不能简单的使用 `os.system()` 或者 `subprocess.call()`来完成．
* 例如:下列方法无法完成

```python
import os
import subprocess
os.system("export OMP_NUM_THREADS=8")
subprocess.call("export OMP_NUM_THREADS=8",shell=True)

```

* 可以使用`os.environ`来导入环境变量

```python
import os
os.environ["OMP_NUM_THREADS"] = "8"

```

# 合并List

* 例如　a = [[a,b],[a,c],[a,d]]

```python
a = [[1,2],[3,4],[1,4]]
b = [x for j in a for x in j]
print b
[1, 2, 3, 4, 1, 4]
```

# List去除重复

* 例如　a = [[a,b],[a,c],[a,d]]

```python
a = [1,2,3,3,4,1]
b = list(set(a))
print b
[1, 2, 3, 4]
```

# 临时文件创建

* python标准库``tempfile``提供了一个临时文件储存的地方，脚本结束自动销毁

```python
import tempfile
temp = tempfile.TemporaryFile() # 实例化
temp.write('create a temp file')　#　写入
temp.seek(0)　# 回到起点位置
print temp.read()
temp.close() #　手动关闭下
```

# 读取文件跳过首行可以用islice

* 有时侯处理文本想跳过首行，也就是header，可以使用islice完成

```bash
$ cat file.txt
name ages
nice 20
pretty 18
```

```python
from itertools import islice

with open('file.txt') as f:
    for i in islice(f, 1, None):
        print
#print
nice 20
pretty 18
```

# Python创建虚拟环境

* Python有一个非常好的设计就是可以创建一个虚拟环境，然后在虚拟环境里面测试，最后删除虚拟环境，这样
设计可以完全与本地Python环境隔开，互不干扰。

## 安装

```python
$ pip install virtualenv
```

## 创建一个虚拟环境

* 创建虚拟环境使用`virtualenv`命令来创建，名字可自己随便命名的。

```python
$ virtualenv ven
```

## 激活虚拟环境

* 激活虚拟环境使用的是`source`命令执行的`bin`下的`activate`即可。激活后会看到终端命令行前有(ven)的标志。

```python
$ source ven/bin/activate
```

## 退出虚拟环境

```python
$ deactivate
```

## 删除虚拟环境

```python
$ rm -rf ven
```

# Python 生成英文字母表

## 手动生成

* 小写字母表

```python
list(map(chr,list(range(97, 123))))

```

* 大写字母

```python
list(map(chr,list(range(65, 91))))

```

##　利用库函数 string

* 小写字母表

```python
import string
string.ascii_uppercase

```

* 大写字母

```python
import string
string.ascii_lowercase

```


# 字典排序

* 按键排序

```python
dic = {'a':11 , 'b':5 , 'c': 7}

# 升序排序
sorted(dic.keys())

#　降序排序
sorted(dic.keys(), reverse=True)

```
* 按值排序

```python
dic = {'a':11 , 'b':5 , 'c': 7}

# 升序
sorted(dic.items(), key = lambda x:x[1])

# 降序
sorted(dic.items(), key = lambda x:x[1],reverse =True)

```

# 获取目录忽略隐藏文件

```python
import os
dir_path = '/home/user/'

filter( lambda f: not f.startswith('.'), os.listdir(dir_path))

```

***

**2017-10-1更新**

***