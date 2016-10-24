---
layout: post
title: R 语言画函数图像
categories: R
description: R如何画一个函数图像
keywords: plot function ,R
---

　　有时候我们想知道一个函数的图像是什么样子的，用R语言很好实现，这里分别用两种方法来实现一种方法是通过 [graphics](https://stat.ethz.ch/R-manual/R-devel/library/graphics/html/00Index.html)包中的
`curve()`函数来实现，一种方法是用[ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html)来实现。

#　分别画sigmoid公式和sin公式

* sigmoid公式:  

![sigmid](http://www.forkosh.com/mathtex.cgi? \Large \frac1{1+e^{-x}})

* sin公式:  

![sin](http://www.forkosh.com/mathtex.cgi? \Large sin(x))


# 用curve()画函数图像

```r
#定义公式
sigmoid <- function(x) 1/(1+exp(-x))

#画sigmid图像
curve(sigmid,-10,10)

#画sin(x)数图像
curve(sin,-10,10)
```

## sigmoid图像

![sigmoid](/images/posts/R/sigmoid_curve.png)

## sin图像
![sin](/images/posts/R/sin_curve.png)

# 用ggplot2绘制函数图像

## 绘制sigmoid函数

```r
library(ggplot2)

# 定义函数
sigmid <- function(x) 1/(1+exp(-x))

# 创建数据点
x<-seq(-5, 5, by=0.01)
y<-sigmid(x)
df<-data.frame(x, y)

# 用ggplot2来画图
g <- ggplot(df, aes(x,y))
g <- g + geom_line(col='red')
g <- g + geom_hline(yintercept = 0.5) + geom_vline(xintercept = 0) #坐标轴
g <- g + ggtitle("sigmoid")
g

```

![sigmoid](/images/posts/R/sigmoid_ggplot2.png)

## 绘制sin函数

```r
library(ggplot2)

# 创建数据点
x <- seq(-5, 5, by=0.01)
y <- sin(x)
df <- data.frame(x, y)

# 用ggplot2来画图
g <- ggplot(df, aes(x,y))
g <- g + geom_line(col='red')
g <- g + geom_hline(yintercept = 0)+geom_vline(xintercept = 0) #坐标轴
g <- g + ggtitle("sin")
g

```

![sigmoid](/images/posts/R/sin_ggplot2.png)