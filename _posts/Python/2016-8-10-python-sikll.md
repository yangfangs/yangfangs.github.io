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


