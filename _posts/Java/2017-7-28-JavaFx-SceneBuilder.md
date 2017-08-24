---
layout: post
title: JavaFx及其在IntelliJ IDEA中配置使用及发布
categories: Java
description: 关于JavaFx配置
keywords: JavaFx, IntelliJ IDEA, SceneBuilder
---

　　学习一下GUI的开发，想来想去几种语言中比较合适的还是Java。有几个优点是其他几种语言无法比拟的。

1. Java语言的跨平台性，Linux，Windows，Mac OS，只要装个Jre，都能运行。

2. 面向对象编程和很多非常优秀的接口可以使用。

3. 性能优秀并不用像使用C语言一样担心内存问题。

4. 与C\++相比,的确C\++实现的GUI更加绚丽和元素更加丰富，但是对于科学计算用的GUI设计，Java足够了。

　　所以学习一下Java的GUI开发，发现Java的GUI开发框架也是不少的，主要流的UGI开发框架有两个：

* [Swing](https://docs.oracle.com/javase/tutorial/uiswing/) 同时有支持可视化开发的 [WindowBuilder](https://eclipse.org/windowbuilder/)

* [JavaFX](http://docs.oracle.com/javase/8/javase-clienttechnologies.htm) 同时有支持可视化开发的 [SceneBuilder](http://www.oracle.com/technetwork/java/javase/downloads/sb2download-2177776.html)

　　JavaFX 是SUN公司在2007年JavaOne大会上首次对外公布，在2001年发布了2.0版本。而AWT和Swing API早在1996(JDK 1.0)年就形成，在1998年JDK 1.2全面添加。JavaFx已经被集成到Java 8的标准库中。所以还是非常值得探究学习的。
本文记录下JavaFX SceneBuilder安装及其在IntelliJ IDEA中的配置

## 需要安装
* [JDK8(Java SE Development Kit 8)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

* [JRE8(Java SE Runtime Environment 8)](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

* [IntelliJ IDEA (Community)](https://www.jetbrains.com/idea/download/#section=windows)

* [JavaFX Scene Builder](http://www.oracle.com/technetwork/java/javase/downloads/sb2download-2177776.html)

## IntelliJ IDEA 中配置 SceneBuilder
  
### 设置 SceneBuilder路径

* 依次打开`File->Setting->Languages&Frameworks->JavaFx`设置启动SceneBuilder的路径

![fig1](/images/posts/java/javafx_install_fig1.png)

### 创建一个JavaFx项目

* 依次打开 `File->New->project`选择JavaFx,如果安装多个版本SDK，选择Java8。

![fig2](/images/posts/java/javafx_install_fig2.png)

### 在IntelliJ IDEA中打开 SceneBuilder

* 创建完成后会自动生成一个样本项目。包括两个类一个逻辑控制类`Controller`和一个主函数类`Main`以及一个`fxml`格式的配置文件，右键点击`fxml`格式文件选择`Open in SceneBuilder`:

![fig3](/images/posts/java/javafx_install_fig2.png)


### 发布JavaFx应用

* 依次打开`File->Project Structure->Artifacts->"+"->JavaFx Application->From module...`

![fig4](/images/posts/java/javafx_install_fig3.png)

* 选择输出地址以及JavaFx选项下面的一些说明都得填写。

![fig5](/images/posts/java/javafx_install_fig4.png)
  
  