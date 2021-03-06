---
layout: post
title: introduction to programming in java学习笔记(3)--数组
categories: Java
description: 关于java的了解
keywords: Java学习,数组
---

## 1.4数组

* 数组即储存着一类相同类型值的序列这就是数组

###一维数组
* 一维数组

![array](/images/posts/java/array.png)

* 在 Java 中创建数组主要有三步:
* 声明一个数组名字和类型
* 创建一个数组
* 初始化这个数组的值
* 例如:

```java
double[] a;
a = new double[N];
for(int i = 0; i < N; i++)
a[i] = 0.0;
```

* 这就是一个简单的三步创建数组,这里需要注意的是你在创建数组时候需要指定数组的大小 N
* 当然这三步在 Java 中常常合并起来写如下:

```java
double[] a = new double[N];
```

* 在 Java 中数组的索引是从 0 开始的指定 N 大小的数组有 N-1 个元素
* 数组的长度可以用 `a.length` 来获得,所以最后一个元素可以用 `a[a.length-1]` 来访问
* 数组在内存中的存储:数组中的元素在内存中是连续排放的,所以你可以很快的访问下标来获取元素内容
* 内存分配:当你是用关键字 new 来创建一个数组时候 Java 就会开辟一个新的内存空间来存放这个数组所以你要明白,开辟内存所花费的时间是与你创建数组大小成正比的
* 边界检查:在使用数组时候一定要注意你存储的数据不要超过了你数组的长度,或者低于 0 这样会使你的程序因为 run-time 异常而终止 `Arraylndex-OutOfBounds`
* 一维数组常用的操作方法如下:

![arrays-examples](/images/posts/java/arrays-examples.png)


### 二维数组
* 二维数组是相当重要的,在数学中可以叫做矩阵,在计算语言中可以用二维数组来表达

![array2d](/images/posts/java/arrays2d.png)

* 创建二维数组很简单如下:

```java
double[] [] a = new double [M] [N];
```

* 二维数组的初始化可以用下面的方法:

```java
doubled [] a;
a = new double[M][N];
for (int i = 0; i < M; i++)
{ // Initialize the ith row.
for (int j = 0; j < N; j++)
a[i][j] = 0.0;
}
```

* 二维数组的输出可以下面的循环来遍历输出:

```java
for (int i = 0; i < M; i++)
{ // Print the ith row.
for (int j = 0; j < N; j++)
System.out.print(a[i][j] +
System.out.pri ntln();
}
```

* 在二维数组中我们可以用 a[i] 来访问数组的第i行但是没有相同的办法来访问一整列:(
* 矩阵的操作
* 例如矩阵相加

```java
double[][] c = new double [N] [N];
for (int i = 0; i < N; i++)
for (int j = 0; j < N; j++)
c[i][j] = a[i][j] + b[i][j];
```

* 矩阵相乘

```java
double[][] c = new double [N] [N];
for (int i = 0; i < N; i++)
{
for (int j = 0; j < N; j++)
{
// Compute dot product of row i and column j,
for (int k = 0; k < N; k++)
c[i][j] += a[i][k]*b[k][j];
}
}
```

### 多维数组
* 初始化一个多维数组如下:

```
doubled [][] a = new double[N] [N] [N];
```


#### 参考书籍

[Introduction to Programming in Java](http://introcs.cs.princeton.edu/java/home/)