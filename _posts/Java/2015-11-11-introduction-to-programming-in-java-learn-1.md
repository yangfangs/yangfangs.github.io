---
layout: post
title: introduction to programming in java学习笔记(1)--数据类型
category: Java
keywords:Java学习,数据类型
description:关于java的了解
---

# introduction to programming in java (一)--数据类型

## 1.1你的第一个程序

* 第一要搭建一个java的开发环境这个可以参考本博客[ubuntu搭建的方法](/_posts/java/2015-11-11-introduction-to-programming-in-java-learn-1.md).

### 1.1.1第一个java程序


![java程序产生的过程](/images/posts/java/compiling.png)

* 一个java程序的的产生需要经过三个步骤.
* 第一步,打开编辑器编辑(editor)你的代码.保存为例如HelloWord.java.
* 第二步,进行编译(compiler)结果例如:HelloWord.class.
* 第三步,执行(excute)你的程序输出结果
* 例如:第一个Java程序

```java
public class HelloWorld{
public static void main(String[] args){

       System.out.print("Hello, World");

       System.out.p rintln();
      }
}
```

* 终端输入
* `javac HelloWorld.java`
* `java HelloWorld`
* 输出结果:`Hello, World`
* 结构解析如下

![HelloWord](/images/posts/java/hello.png)

### 1.1.2可传入参数的java程序

```java
public class UseArgument {

    public static void main(String[] args) {
        System.out.print("Hi, ");
        System.out.print(args[0]);
        System.out.println(". How are you?");
    }

}
```

* 终端输入
* `javac UseArgument.java`
* `java UseArgument job`
* 显示结果:`Hi, job. How are you?`
* 这是一个非常简单的在终端读入参数然后打印出来的java程序.虽然简单但其机制是非常经典的,java编辑器无非作为一个程序输入一个字符串然后将其输入.这对后来写更复杂的机制程序提供了很好基础.

## 1.2内建的数据类型
	
* java内建的数据类型很多常用的有五种:对于整数有整型(int)、对于实数有双精度型(double)、对于真和假的判断有布尔型(boolean)、对于字符有字符型(char)、对于字符串有字符串型(String).基本数据类型有8个分别是 boolean, char, byte, short, int, 1ong, f1oat, double.
* 五种常用的内建类型

![数据类型](/images/posts/java/built-in.png)

* **将命令行参数中的字符串转换成基本值**
* java中有两个方法` Integer.parseIntO`和`Double.parseDouble`
* 例如:`Integer.parseInt(args[])`
* **将结果转换成将字符串输出**
* 在java可以很容易的将任意基本数据类型转自动换成字符串,需用到一个`+`操作符
* 例如:`a = "1"`,`b = 2`,`c = a + b`结果就自动转换成了字符串"3"
* **方法库(Library methods)和接口(APIs)**
* 方法库和接口的存在是java变得超级强大,当然这也是非常的庞大需要在以后的使用中慢慢学习
* 例如一个方法库`public clss System.out`涵盖的方法有`void print(String s)`、`void println(String s)`、`void println()`等方法让我们使用
* 例如一个接口`public class Math`涵盖有`double abs(double a)`、`double max(double , double b)`、`double random()`等很多接口方法,这里值得注意的是除了`double random()`其他的接口都是实现类的方法,因为`random()`没有接受参数,当然`void print(String s)`等方法也不是实现类方法,因为他们没有返回值
* 使用这些方法

```java
double d = Math.sqrt(b*b - 4.0*a*c);
```

### 数据类型的转换

![casts](/images/posts/java/casts.png)

* **显示类型转换(Explicit type conversion)**
* 例如:使用`Integer.parseInt`和`Double.parseDouble`直接将字符串数值转换成整型和双精浮点型度型
* **显示转换(Explicit cast)**
* 例如:`(int)2.71828`通过这种方法把浮点型转换成了整型
* **数字自动转型(Automatic promotion for numbers)**
* 对于java来你可以使用任意基本类型数字,当这些数字可能超过设定类型范围时候,java会自动转型为较大范围的类型这就叫做promotion

####	参考书籍

[Introduction to Programming in Java](http://introcs.cs.princeton.edu/java/home/)
