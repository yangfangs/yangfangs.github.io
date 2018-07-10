---
layout: post
title: Python 中科学计算库 scipy 中距离的计算
categories: Python
description: python scipy
keywords: python, scipy, distance
---

　　计算两两向量间的距离或者相似度， Python 和 R 都有相当成熟的库可以用，这里学习一下 Python 库[scipy][1]中关于距离的计算方法。


# 安装库

```bash
pip install numpy
pip install scipy
```

# 使用

* scipy 库关于距离的计算提供了 `jaccard`、 `hamming` 等22种方法来计算两两向量间的距离，这里用 `jaccard` 为例：

```python
import numpy as np
import scipy.spatial.distance as dist
matV = np.mat([[1, 1, 1, 1],
               [1, 1, 1, 1],
               [1, 0, 0, 1]
               ])
dis = dist.pdist(matV, 'jaccard')
print dis
array([ 0. ,  0.5,  0.5])
```


# 距离与行对应提取

* 一种方法来提取矩阵的行名与计算结果一一对应

```python
copy_node = ["A","B","C"]
index = 0
while (copy_node):
    node = copy_node.pop(0)
    for line in copy_node:
        print(node, line, dis[index])
        index += 1
```

* `scipy`计算距离是通过C语言API实现的，底层用C写的所以计算速度有保证，很快，实测计算2亿次距离不到2分钟计算完毕。





[1]: http://www.scipy.org/