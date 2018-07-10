---
layout: post
title: Python 测试单元 unittest 使用
categories: Python
description: python unittest
keywords: python unittest
---

　　学习一下 Python 单元测试方法,这里使用的是 PyUnit 框架

# 测试模块中的函数

##  被测试模块

```python
class myclass():
    def __init__(self):
        pass
    def add(self, x, y):
        return x+y
    def dou(self, x):
        return x*2

```


## 单元测试模块

```python
import unittest
import myclass

class mytest(unittest.TestCase):

    ##初始化工作
    def setUp(self):
        self.t_class = myclass() # test实例化

    #退出清理工作
    def tearDown(self):
        pass

    #具体的测试用例，最好以test开头，这样可以被main()识别然后统一测试
    def test_sum(self):
        self.assertEqual(self.t_class.add(1, 1), 2, 'test add pass')

    def test_dou(self):
        self.assertEqual(self.t_class.dou(3), 6, 'test add pass')

if __name__ =='__main__':
    unittest.main()
```



# run

```pyton
..

..

----------------------------------------------------------------------
Ran 2 tests in 0.001s

OK


Process finished with exit code 0

```



# 参考

* [Python自动单元测试框架PyUnit](http://www.oschina.net/question/12_27127#TESTCONDS)
* [IBM Python自动单元测试框架](http://www.ibm.com/developerworks/cn/linux/l-pyunit/)
* [python 测试的几种框架](http://www.tuicool.com/articles/2uIv6v2)