---
layout: post
title: Python 中的一些小技巧
categories: Python
description: Python skill
keywords: Development, Skill, Python
---

　　积累一些在使用Python中能用到的一些技巧！


# 生成一个独一无二的时间文件夹

```Python
import time
timeformat = '%Y%m%d%H%M%S'
timeinfo = str(time.strftime(timeformat))
timeinfo
'20160810180815'
```

# 去除list中的空字符串

例如 `a = ['a','b','','c']`　去除其中的空字符串

```Python
def removeEmptyString(inputlist):
    temp = []
    for line in inputlist:
        if line:
            temp.append(line)
    return temp
```

# 定位当前脚本的绝对路径

```Python
import os
def getlocalpath():
    relpath = os.path.split(os.path.realpath(__file__))[0]
    return relpath
```

# 判断目录若不存在则创建

```Python
import os
if not os.path.exists(dirname):
    os.makedirs(dirname)
```

