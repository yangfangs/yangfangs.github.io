---
layout: post
title: Markdown 简明语法
categories: Linux
description: Markdown语法
keywords: Markdown, Linux
---

## 编辑器

* 我认为想用Markdown来作为以后的主要写作工具,有一个称心如意的编辑器是不可少的,我在Linux下用的是 [Haroopress](http://pad.haroopress.com/) ,是一个非常酷的编辑器,如果你也准备用 Markdown 不妨尝试一下,有着 Sbulime text 的启动速度,还有自动补全功能,是一个写作的好帮手,当然是同时支持Linux、Windows、Mac、三个操作系统的.

* **Haroopress**

![Haroopress](http://pad.haroopress.com/assets/images/intro/1.png)

## 基本符号

* *,-,+ 三个符号效果都是一样的,这三个符号被称为 Markdown 符号
* 空白行表示另起一个段落
*  \` 表示 inline 代码, tab 是用来标记代码段当然 \``` 更好用,分别对应 html 的 code , pre 标签 \
  
***

* 例如:
* \*\*粗体\*\*
* 显示效果:**粗体**
* \*斜体\*
* 显示效果:*斜体*
* \`inline\`
* 显示效果:`inline`

***

## 换行

* 单一段落( <\p> )用一个空白行
* 连续两个空格会变成一个<\br>
* 连续三个符号,然后空行,表示hr横线

***

* 例如:
* 三个\*\*\*表示page break
* 三个\-\-\-表示section break
* 三个\_\_\_表示 sectence break

***

## 标题

* 生成 h1-h6 ,在文字前面加上 1--6 个#来实现
* 文字加粗是通过文字前后各两个 \* 来实现的,斜体是前后一个\*实现的,下划线是前后两个 \+ 来实现的

***

* 例如:
* \#一级标题
* 显示效果:

# 一级标题

* \##二级标题
* 显示效果:

## 二级标题

***

## 引用

* 在第一行加上 ">" 和一个空格,来表示代码引用,还可以嵌套呢

***

* 例如: \> 引用
* 显示效果:
* >引用

***

## 列表

这是Markdown文件的主要表示方式,主题要点化

* 使用*,+,-加上一个空格来表示
* 可以支持嵌套
* 有序列表用"数字+英文点+空格来表示
* 列表内容很长,不需要手工输入换行符,css控制段落的宽度,会自动缩放的

***

* 例如

\| 姓名 \| 年龄 \|

\|------\|------\|

\| 小明 \| 25  \|

* 显示效果

| 姓名 | 年龄 |
|------|-----|
| 小明 |  25  |

***

## 链接

* 直接可以用 \[锚文本](url"可选的title")
* 引用先定义 [ref_name]:url ,然后需要写入url的地方,使用 [锚文本][ref_name] ,通常的 ref_name 一般用数字表示,这样显得专业
* 图片插入使用 \!\[alt text](url) 来实现

***

* 例如 \[google](www.google.com)
* 显示效果
* [google](www.google.com)

***

## 特殊符号

* 用 \ 来转义,表示文本中的Markdown符号
* 可以在文本中直接使用html标签,但是要注意使用的时候前后要加上空行
* 文本前后各加一个符号,表示斜体

# 一些常用的Markdown语法

## 删除线

* 需要对删除的文本前后用 ~~ 来加删除线
* 例如:
* \~\~ 这是要删除的内容 \~\~
* 显示效果
*  ~~这是要删除的内容~~

## 代码块高亮

* 使用三个 ``` 包围代码块就可以了,而被包围的代码快是不需要任何的缩进的,这种方式也称为"围栏试代码块"
* 例如:

\`\`\`Python

print("Hello World")
 
\`\`\`  

* 显示效果

```python
print("Hello World")
```

>GitHub发布公告从 2016 年 5 月 1 日起，GitHub Pages 只专属用 kramdown 作为 Markdown 引擎了这与 Redcarpet 解析的稍微有不同,具体不同参考[kramdown Syntax](http://kramdown.gettalong.org/syntax.html)

# markdown文档插入公式

## 1.使用Google Chart的服务器

* 由于国内限制不太好使

```
<img src="http://chart.googleapis.com/chart?cht=tx&chl= 在此插入Latex公式">
```

例如:

```
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">
```

显示如下:  

![function](http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})


## 2.使用使用forkosh服务器

~~* 这个国内网速还行。~~


~~\<img src="http://www.forkosh.com/mathtex.cgi? 在此处插入Latex公式">~~



~~例如:~~


~~\<img src="http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">~~


~~显示如下:~~

![function](http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a})


* forkosh提供了一个能帮助你快速写出Latex公式的网站:[mathtextutorial](http://www.forkosh.com/mathtextutorial.html)。


**waring:这种方法已经不能使用了**

## 3.使用使用MathJax引擎

* [MathJax](https://www.mathjax.org/)引擎还是相当好用的,首先需要在Markdown中引入一段javascript代码然后就可以书写了

* 引入代码如下:

```
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
```

书写使用``$$公式$$``的方式来出入公式例如：

```
$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$
```

显示如下:

$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$

# Markdown插入邮箱链接

* Markdown是可以直接解析html的，所以可以直接在markdown中写入html来实现插入邮箱链接，通过这种方式插入链接可以实现点击发邮件。

例如:

```html
<a href="mailto:testmail@gmail.com">testmail@gmail.com</a>
```

效果如下：
<a href="mailto:teastmail@gmail.com">testmail@gmail.com</a>




### 相关参考:

* [Markdown 语法说明 (简体中文版)](http://www.appinn.com/markdown/)
* [Markdown 是什么和我为什么用 Markdown](http://www.fallhunter.com/p/10605)
* [Kramdown 语法](http://kramdown.gettalong.org/syntax.html)
* [Markdown 中插入数学公式的方法](http://blog.csdn.net/xiahouzuoxin/article/details/26478179)
* [MathJax](https://www.mathjax.org/)
* [mathtextutorial 一个学习LaTeX的好地方](http://www.forkosh.com/mathtextutorial.html)