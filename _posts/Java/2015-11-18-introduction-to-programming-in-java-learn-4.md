---
layout: post
title: introduction to programming in java学习笔记(4)--输入和输出
categories: Java
description: 关于java的了解
keywords: Java学习,输入和输出
---

# 1.5输入和输出

## 鸟瞰

* **命令行输入**
* 所有的类有一个主函数`main()`方法这个方法可以接受一个字符串数组 args[] 作为它的参数,这个参数就是我们在命令行下输入的,由操作系统提供给Java的参数,为了方便 Java 和操作系统都把这些参数作为字符串来处理,当然如果我们想输入数字需要是需要使用例如 `Integer.parseInt()` 或者 `Double.parseDouble()` 的方法来把输入的字符串转换成数字.
* **标准输出**
* 为了打印我们程序的值所以需要输出,已经用过的有: `System.out.println()`、`System.out.print()` 等 Java 是以一种抽象字符流的形式来输出这些值作为标准输出
* 一个简单的输入输出例子:

```java
public class RandomSeq {
    public static void main(String[] args) {

        // command-line argument
        int N = Integer.parseInt(args[0]);

        // generate and print N numbers between 0 and 1
        for (int i = 0; i < N; i++) {
            System.out.println(Math.random());
        }
    }
}
```

## 三个标准库

* **标准输入输出**
* `StdIn` 和 `StdOut` 类是一个可以实现标准输入抽象到标准输出抽象的一个完整的过程.正如你可以在执行程序时候通过标准输出随时打印你的程序值,当然你也可以在任何时候通过输入流来读取你的值
* 下载到你程序所在的文件夹使用 [StdIn.java](http://introcs.cs.princeton.edu/java/15inout/StdIn.java.html) 和 [StdOut.java](http://introcs.cs.princeton.edu/java/15inout/StdOut.java.html)
* **标准画图**
* `StdDraw`类允许你使用程序来画图.这允许你在计算机窗口创建简单的点和线等图形,`StdDraw`当然也包括了文本,颜色,动画等工具
* 下载到你程序所在的文件夹使用 [StdDraw.java](http://introcs.cs.princeton.edu/java/15inout/StdDraw.java.html)
* **标准音频**
* `StdAudio`类允许使用程序来创建音频.这使用标准的格式来转换数字类型数组成声音
* 下载到你程序所在的文件夹使用 [StdAudio.java](http://introcs.cs.princeton.edu/java/15inout/StdAudio.java.html)
* 标准输入输出的使用例子:

```java
public class AddInts { 
   public static void main(String[] args) { 
      int N = Integer.parseInt(args[0]); 
      int sum = 0; 
      for (int i = 0; i < N; i++) 
         sum += StdIn.readInt(); 
      StdOut.println("Sum is " + sum); 
   } 
} 
```



#### 参考书籍

[Introduction to Programming in Java](http://introcs.cs.princeton.edu/java/home/)