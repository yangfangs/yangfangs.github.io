---
layout: post
title: Python并行计算
categories: Python
description: Python　并行计算　multiprocessing
keywords: map, multiprocessing, Python3
---


　　当你在使用 Python 进行 for 循环时候，发现计算的效率及其慢的时候，完全可以考虑使用 Python 的并行操作，毕竟这么多核心不用也是一种浪费。还有 Python 标准库提供了并行库相当的简洁好用。


# Python中的标准库
 
　　Python 标准库中有两个提供并行计算一个是[multiprocessing](https://docs.python.org/3.6/library/multiprocessing.html), 另一个是 [threading](https://docs.python.org/3.6/library/threading.html),推荐使用 multiprocessing, 当只有I/O密集型操作时候才有用到threading的必要。当然由于 Python 的 [Global interpreter lock](https://docs.python.org/2.7/glossary.html#term-global-interpreter-lock)存在，导致 Python 不能进行并行编程，只能进行并发编程。
  
# 多进程`multiprocessing`的使用

* multiprocessing模块还是非常好用的。

## 单参数函数执行并计算

```python
import multiprocessing

def f(x):
    return x*x

# Get all cores
cores = multiprocessing.cpu_count()
# start a pool
pool = multiprocessing.Pool(processes=cores)

tasks = [1,2,3,4,5]

# do parallel calculate
print(pool.map(f,tasks))

```

> 其实`map`函数在执行的时候就已经是并行操作了，只不过`multiprocessing`模块集成了`map`方法

## 多参数函数执行并行计算

### Python3 中使用`starmap`方法来实现

```python
import multiprocessing

def add(x, y):
	return x+y

# Get all worker processes
cores = multiprocessing.cpu_count()

# Start all worker processes
pool = multiprocessing.Pool(processes=cores)
x1 = list(range(5))
y1 = list(range(5))

tasks = [(x,y) for x in x1 for y in y1]

print(pool.starmap(add,tasks))

```

### Python2 中需要一个函数对多参数函数包装下


```python
import multiprocessing

def add(x, y):
	return x+y

def merge_add(args):
	return add(*args)


# Get all worker processes
cores = multiprocessing.cpu_count()

# Start all worker processes
pool = multiprocessing.Pool(processes=cores)
x1 = list(range(5))
y1 = list(range(5))

tasks = [(x,y) for x in x1 for y in y1]

print(pool.map(merge_add,tasks))

```

# 参考

* [Python multiprocessing for mutiple arguments](https://stackoverflow.com/questions/5442910/python-multiprocessing-pool-map-for-multiple-arguments)
* [multiprocessing](https://docs.python.org/2/library/multiprocessing.html)

