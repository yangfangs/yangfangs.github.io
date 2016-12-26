---
layout: post
title: Python和C语言的交互
categories: Python
description: python C语言
keywords: python, C语言，交互, ctypes
---

　　最近算一个矩阵，计算大约为２亿对节点的距离，用`Python`的循环输出结果，用了大概40分钟把结果写入文本中，而使用，`scipy`的库计算
距离，仅仅用了不到两分钟，无比感慨，差距怎可如此之大。翻看scipy库的源代码，计算距离是用C语言实现的，激发对Python和C语言交互的研究的
热情。记录一下方法，日后会用到。


# 通过`ctypes`直接调用C的标准动态库

## 1.加载C标准动态库方法

```python
from ctypes import cdll
#Linux下
libc = cdll.LoadLibrary('libc.so.6')  # Load standard C library on Linux
# Mac下
libc = cdll.LoadLibrary('libc.dylib')
# Win 下
libc = cdll.msvcrt
````

## 2.调用C标准库函数
```python
# C标准库printf函数
libc.printf("%s",'cprintf')

#调用标准库中的time
print libc.time(None)

#调用C标准库atoi()
print libc.atoi("1234")
```


## 3.ctypes 数据类型和 C数据类型 对照表


| ctypes type  | C type                                 | Python type                |
|--------------+----------------------------------------+----------------------------|
| c_bool       | _Bool                                  | bool (1)                   |
| c_char       | char                                   | 1-character string         |
| c_wchar      | wchar_t                                | 1-character unicode string |
| c_byte       | char                                   | int/long                   |
| c_ubyte      | unsigned char                          | int/long                   |
| c_short      | short                                  | int/long                   |
| c_ushort     | unsigned short                         | int/long                   |
| c_int        | int                                    | int/long                   |
| c_uint       | unsigned int                           | int/long                   |
| c_long       | long                                   | int/long                   |
| c_ulong      | unsigned long                          | int/long                   |
| c_longlong   | __int64 or long long                   | int/long                   |
| c_ulonglong  | unsigned __int64 or unsigned long long | int/long                   |
| c_float      | float                                  | float                      |
| c_double     | double                                 | float                      |
| c_longdouble | long double                            | float                      |
| c_char_p     | char * (NUL terminated)                | string or None             |
| c_wchar_p    | wchar_t * (NUL terminated)             | unicode or None            |
| c_void_p     | void *                                 | int/long or None           |

## 4.创建ctypes类型

* 使用`.value`取值和修改值

```python
from ctypes import *
#　创建和取值
x = c_int(2)
print x.value
char = c_char_p("Hello, World")
print char.vaule

# 改变值
x.value = 3
print x.value
```

## 5.函数返回类型

* 默认返回C int类型，可以使用restype设置返回类型

```python
strchr = libc.strchr
print strchr("hello", ord("e"))
-1003868475
strchr.restype = c_char_p # c_char_p is a pointer to a string
print strchr("hello", ord("e"))
ello
```

## 6.定义数组

```
intarr = c_int * 10
a = intarr(1,2,3)
# 取值
a[0]
1
```



# 编译自己的动态链接库

* 下面是直接使用Python的ctypes来直接调用C编译后的函数

# 1.首先写个C函数`libtest.c`

```c
int addnum(int num1, int num2)
{
  return num1 * num2;
}
```

# 2.编译动态链接库

```bash
gcc -shared libtest.c -o libtest.so

```

# 3.调用

```python
from ctypes import *
import os
libtest = cdll.LoadLibrary(os.getcwd() + '/libtest.so')
print libtest.addnum(1, 2)

```


# 第二种方法用C提供的API扩展Python

* `scipy`就是这么干的，比较复杂，当然越是复杂的方法用法就越灵活。

* 两篇不错的参考

[引用1][1]

[引用2][2]











# 参考

[Extending Python with C or C++][1]

[用C语言扩展Python的功能][2]

[ctypes][3]


[1]: https://docs.python.org/dev/extending/extending.html

[2]: https://www.ibm.com/developerworks/cn/linux/l-pythc/

[3]: https://docs.python.org/3/library/ctypes.html