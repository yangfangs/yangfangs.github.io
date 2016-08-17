---
layout: post
title: RGB和16进制颜色(HEX)相互转换
categories: Python
description: RGB和HEX颜色转换
keywords: RGB, HEX, covert
---

　　　想在 Python 随机生成16进制的颜色代码，找来找去没有发现好的包，于是自己写了一个生成　HEX 的颜色脚本，方便使用，还不用依赖第三方库。


#  理论部分 


## HEX 转换 RGB　算法

* 从 HEX 表示颜色转换成　RGB 方法表示颜色，是`HEX的第一位数乘以16加上第二位数`举个例子:转换颜色为 `#1722DF`的 HEX 值到 RGB 值　

```
#1722DF ----------> rgb:

17 --------------> r: r的值就是: 1 * 16 + 7 = 23

22 --------------> g: g的值就是:　2 * 16 + 2 = 34

DF --------------> b: b的值就是: 16 * 13 + 15 = 223
```

* 所以 `#1722DF`　转换为RGB的表示的值为 `(23,34,223)`


## RGB 转换成 HEX　的算法


* 从 RGB 转换成 HEX　表示颜色是　HEX　到 RGB　值的一个逆过程 `对RGB的值分别除以16商加上余数就是HEX值了`其中0对应的为00例如：转换(0,223,55)到HEX值

```
(0,223,55) --------> hex:

0 -----------------> 00：　0对应00

223 ---------------> DF： 223 / 16 = 13 余　15`

55 ----------------> 37:  55 / 16  = 3 余　7
```


## 16进制16个数超过10对应关系:


* `0~9` 依次为对应二进制的 `0~9`

* 超过10的部分对应关系：

```
11 ------------> A
12 ------------> B
13 ------------> C
14 ------------> D
15 ------------> E
16 ------------> F
```

# Python 实现 RGB 和 HEX 相互转换：

```python
def convert(value):
    """
    convert 2------>16
    :param value: input int type
    :return: str type(16)
    """
    if value == 10:
        return "A"
    elif value == 11:
        return "B"
    elif value == 12:
        return "C"
    elif value == 13:
        return "D"
    elif value == 14:
        return "E"
    elif value == 15:
        return "F"
    return str(value)


def convert_hex(value):
    """
    convert 16------2
    :param value: input string type
    :return: str type(2)
    """
    if value == "A":
        return str(10)
    elif value == "B":
        return str(11)
    elif value == "C":
        return str(12)
    elif value == "D":
        return str(13)
    elif value == "E":
        return str(14)
    elif value == "F":
        return str(15)
    return str(value)


def rgb2hex(rgb):
    """
    Convert RGB to HEX color
    :param rgb: Rge value example(23,32,44)
    :return: Hex value example #??????
    """
    hex = []
    for i in rgb:
        if i == 0:
            h = str(0) + str(0)
        else:
            h_left = i / 16
            h_right = i % 16
            h = convert(h_left) + convert(h_right)

        hex.append(h)
    hex_combine = "#" + ''.join(hex)
    return hex_combine


def hex2rgb(hex_value):
    """
    Convert hex to rgp
    :param hex_value: string type example "#1722DF"
    :return: a rgb color tuple example (23,34,223)
    """
    hex = hex_value[1:]
    hex_splite = [convert_hex(x) for x in hex if x]
    hex_splite_rgb = splite_string(hex_splite, 2)
    rgb = [int(line[0]) * 16 + int(line[1]) for line in hex_splite_rgb if line]
    return tuple(rgb)

def splite_string(s, n):
    return [s[i:i + n] for i in range(len(s)) if i % n == 0]

```


# 测试转换


```python
hex2rgb("#1722DF")

(23, 34, 223)

rgb2hex((0,223,55))

'#00DF37'

```



参考：

* [RGB颜色与16进制颜色换算方法](http://blog.csdn.net/jia635/article/details/24935491)