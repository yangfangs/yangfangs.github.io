---
layout: post
title: Java 创建销毁对象——静态工厂方法
categories: Java
description: 静态工厂方法
keywords: static factory method
---


  什么是静态工厂方法？在 Java 中，获得一个类实例常常使用 new 关键字，通过构造函数来实现对象的创建。不通过 new，
而是用一个静态方法来对外提供自身实例的方法，即为**静态工厂方法(Static factory method)**。

#  使用静态工厂方法的优势

* Effective Java中有如下总结:
1. 静态工厂方法与构造器不同的第一优势在于，它们有名字。
2. 不必在每次被调用时都创建新对象。
3. 可以返回原返回类型的任何子类对象。
4. 在创建参数化类型实例的时候，能使代码变得简洁。

#  1.静态工厂方法与构造器不同的第一优势在于，它们有名字

* 例如：Boolean类的一个构造方法，以及通过该构造方法创建一个Boolean对象；

```java

public Boolean(String s) {
        this(toBoolean(s));
    }

Boolean bTrue = new Boolean("true");

```

* 使用静态工厂方法可以如下

```java

public static Boolean valueOf(String s) {
        return toBoolean(s) ? TRUE : FALSE;
    }

Boolean bTrue = Boolean.valueOf("true");

```

在这里我们使用 valueOf 在实例化一个对象，并没有使用 new 关键字，同时实例化时候使用了新的名称 `valueOf` 而不是 `Boolean`构造器的名称。


#  2.不必在每次被调用时都创建新对象


* JDK中的Boolean类的valueOf方法就是使用这个优势，在Boolean类中，有两个事先创建好的Boolean对象（True,False）（静态类的原因），并不是每次调用时候在重新创建，增加 JVM 开销

*  例如：

```java

public final class Boolean implements java.io.Serializable,
                                      Comparable<Boolean>
{
    /**
     * The {@code Boolean} object corresponding to the primitive
     * value {@code true}.
     */
    public static final Boolean TRUE = new Boolean(true);

    /**
     * The {@code Boolean} object corresponding to the primitive
     * value {@code false}.
     */
    public static final Boolean FALSE = new Boolean(false);

```

* 使用Boolean.valueOf("true")静态工厂方法调用时候返回的就是这两个实例的引用。这样可以避免每次调用都自重复创建对象。

```java

    public static Boolean valueOf(String s) {
        return toBoolean(s) ? TRUE : FALSE;
    }
```


#  3.可以返回原返回类型的任何子类对象。

* 我们在选择返回对象的类时，使用静态工厂方法就更有灵活性。这种灵活性的一种应用是API可以返回对象，同时又不会使对象的类变成公有的。这种方式隐藏实现类会使API变得非常简洁。
对于构造方法只能返回确切的自身类型，而静态工厂方法则能够更加灵活，可以根据需要方便地返回任何它的子类型的实例。

* 例如:

```java

Class Person {
    public static Person getInstance(){
        //直接返回子类
        return new Player()
        // return new Cooker()
    }
}
// 子类
Class Player extends Person{
}
// 子类
Class Cooker extends Person{
}

```

#  4.在创建参数化类型实例的时候，能使代码变得简洁。

* 主要对与泛型书写简化：

* 例如：

```java

Map<String,Date> map = new HashMap<String,Date>();

//更加简洁，不需要重复指明类型参数，可以自行推导出来
Map<String,Date> map = new HashMap.newInstance();

```
Java7以后的版本对于一个已知类型的变量进行赋值时，由于泛型参数是可以被推导出，所以可以在创建实例时省略掉泛型参数。所以这个优势实际上以及不存在了。

# 静态工厂方法额外的用处


## 1.可以有多个参数相同但名称不同的工厂方法

* 例如:

```java
class Child{
    int age = 10;
    int weight = 30;
    public static Child newChild(int age, int weight) {
        Child child = new Child();
        child.weight = weight;
        child.age = age;
        return child;
    }
    public static Child newChildWithWeight(int weight) {
        Child child = new Child();
        child.weight = weight;
        return child;
    }
    public static Child newChildWithAge(int age) {
        Child child = new Child();
        child.age = age;
        return child;
    }
}

```

##  2.可以减少对外暴露的属性

* 这种方法也常常使用枚举来代替常量值来设置，当然如果不想用枚举的话，静态工厂方法也是一个很好的办法。

* 例如：

```java

class Player {
    public static final int TYPE_RUNNER = 1;
    public static final int TYPE_SWIMMER = 2;
    public static final int TYPE_RACER = 3;
    int type;

    private Player(int type) {
        this.type = type;
    }

    public static Player newRunner() {
        return new Player(TYPE_RUNNER);
    }
    public static Player newSwimmer() {
        return new Player(TYPE_SWIMMER);
    }
    public static Player newRacer() {
        return new Player(TYPE_RACER);
    }
}

```

#  参考:

[Effective java 中文版（第2版）](https://book.douban.com/subject/3360807/)

[关于 Java 的静态工厂方法，看这一篇就够了](https://www.jianshu.com/p/ceb5ec8f1174)