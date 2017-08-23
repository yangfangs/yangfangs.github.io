---
layout: post
title: python 中 map(), filter(), reduce() 和 zip() 函数的用法
categories: Python
description: python list操作函数的用法
keywords: python,map(),filter(),reduce(),zip()
---

　　Python 自带模块的数据结构屈指可数，list是一个随时都在用的数据结构，对list进行操作python内置了几个函数对python的list进行操作时候非常方便。


# map()函数——作用于list每一个元素

* map()是 Python 内置的高阶函数，它接收一个函数 f() 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。(这个函数与 R 中的 lapply 非常相似)

* 用法map(function, sequence)

## 轻松转换 list 中元素类型：

* 例如 chr 类型转换成 int

```python

l = ['1','2','3','4']
list(map(int,l))

Out[2]: [1, 2, 3, 4]
```

## 编写独立函数作用与 list 中每一个元素：

* 例如对 list 中每一个元素求平方

```python
def f(x):
    return x**2

l =[1,2,3,4]

list(map(f,l))

Out[3]: [1, 4, 9, 16]
```

## 使用匿名函数操作：

```python
l =[1,2,3,4]
list(map(lambda x: x**2, l))

Out[4]: [1, 4, 9, 16]
```

## 同时操作两个 list(并行非多核运算)

```python

l =[1,2,3,4]
list(map(lambda x,y: x+y,l,l))

Out[5]: [2, 4, 6, 8]

```

> 注：python3 和 python2 中map()的返回值不一样， python2 中直接返回列表，python需要加list()转换取值。

# filter()函数——筛选函数

* 按照 function 函数的规则在列表 sequence 中筛选数据
* 用法：filter(function, sequence)

## 筛选 list 中符合条件的值

```python
l =[1,2,3,4]
filter(lambda x: x>2, l)

Out[6]: [3, 4]
```

## filter() 与 map() 返回值不同

```python
l =[1,2,3,4]
map(lambda x: x>2, l)

Out[8]: [False, False, True, True]
```

# reduce()——求积累运算

* reduce函数功能是将 sequence 中数据，按照 function 函数操作，如将列表第一个数与第二个数进行 function 操作，得到的结果和列表中下一个数据进行 function 操作，一直循环下去…

* 用法reduce(function, sequence):

## 求积累和

```python
l =[1, 2, 3, 4]
reduce(lambda x,y: x+y, l)

Out[10]: 10

```

# zip()打包函数

* zip()是 Python 的一个内建函数，它接受一系列可迭代的对象作为参数，将对象中对应的元素打包成一个个tuple（元组），然后返回由这些tuples组成的list（列表）。若传入参数的长度不等，则返回 list 的长度和参数中长度最短的对象相同。利用*号操作符，可以将list unzip（解压）。

* 用法: zip(list,list)

## zip()基本用法

```python
l1 = [1, 2, 3, 4]
l2 = ['a', 'b', 'c', 'd']

zip(l1,l2)
Out[12]: [(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd')]


```

## 使用`*`逆过程

```python
l1 = [1, 2, 3, 4]
l2 = ['a', 'b', 'c', 'd']
zip_l1_l2 = zip(l1,l2)
zip(*zip_l1_l2)

Out[17]: [(1, 2, 3, 4), ('a', 'b', 'c', 'd')]

```

## zip 构造字典

```python
l1 = [1, 2, 3, 4]
l2 = ['a', 'b', 'c', 'd']
zip_l1_l2 = zip(l1,l2)

dict(zip_l1_l2)

Out[18]: {1: 'a', 2: 'b', 3: 'c', 4: 'd'}
```