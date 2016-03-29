---
layout: post
title: 用 ggplot2 画折线图
categories: R
description: ggplot画图
keywords: ggplot2,R
---

　　用[ggplot2](https://github.com/hadley/ggplot2)在[R](https://www.r-project.org/)中画图,能够画出非常漂亮的统计图,由于 ggplot2 的作者 Hadley Wickham 在开发 ggplot2 的时候借鉴了 Photoshop 的图层的思想,使得利用ggplot2来画图,非常方便的维护和修改,画出来的图只需要修改每个图层的数值就行了,而不需求全面修改。

  Hadley Wickham 在 R 社区可是一个大神级别的人物,一个 ggplot2 包可以说让 R 火的不行,什么还不知道 Hadley Wickham 长什么样?没关系[戳我](https://avatars3.githubusercontent.com/u/4196?v=3&s=400)你就认识他了。

  学习 ggplot2 可不是一件太容易的事情,就这个 package 的[书](http://www.amazon.com/dp/0387981403/ref=cm_sw_su_dp?tag=ggplot2-20)就有 200 页,先学习下折线图,不过各种图原理都差不多,记录下画折线图的流程,方便下次再画类似的图。

### 1.数据准备

* 准备好一个`data.frame`格式的数据
* 画一个物种随着月份出现概率的折现统计

```r
library(ggplot2)
set.seed("123")
month <- c(1,2,3,4,1,2,3,4)
count <- runif(8)
species <- c('A','A','A','A','B','B','B','B')
mydata <- data.frame(month,count,species )

```
* 生成的mydata数据如下

```
  month         count species
1     1 0.28757752012       A
2     2 0.78830513544       A
3     3 0.40897692181       A
4     4 0.88301740400       A
5     1 0.94046728429       B
6     2 0.04555649939       B
7     3 0.52810548805       B
8     4 0.89241904439       B

```


### 2. 生成折线图

```r
p <- ggplot(mydata,aes(x=month,y=count,colour=species,group=species,fill=species)) +
			geom_line(size =0.8)
p
```


### 3.各种添加和修改

#### 添加圆点符号---加图层 `geom_point()`


```r
p <- ggplot(mydata,aes(x=month,y=count,colour=species,group=species,fill=species)) +
			geom_line(size =0.8)+ 
				geom_point(size=1.5)
p
```

![plot_broken_line2](/images/posts/R/plot_broken_line2.png)


#### 添加各点的数值---加图层 `geom_text()`


```r
p <- ggplot(mydata,aes(x=month,y=count,colour=species,group=species,fill=species)) +
			geom_line(size =0.8)+ 
				geom_point(size=1.5)+
				    geom_text(aes(label = count, vjust = 1.1, hjust = 0.5, angle = 0), show.legend = FALSE)
p
```

![plot_broken_line3](/images/posts/R/plot_broken_line3.png)


#### 修改x轴坐标点的名字---加图层 `geom_x_continuous()`


```r
p <- ggplot(mydata,aes(x=month,y=count,colour=species,group=species,fill=species)) +
			geom_line(size =0.8)+ 
				geom_point(size=1.5)+
				    geom_text(aes(label = count, vjust = 1.1, hjust = 0.5, angle = 0), show.legend = FALSE)+
				          scale_x_continuous(breaks=c(1,2,3,4), labels=c("January", "February", "March", "April"))
p
```

![plot_broken_line4](/images/posts/R/plot_broken_line4.png)


#### 修改坐标轴的标签和添加标题---加图层 `labs(x = , y = , title = )`

* 或者`xlab()` + `ylab()` + `ggtitle()`

```r
p <- ggplot(mydata,aes(x=month,y=count,colour=species,group=species,fill=species)) +
			geom_line(size =0.8)+ 
				geom_point(size=1.5)+
				    geom_text(aes(label = count, vjust = 1.1, hjust = 0.5, angle = 0), show.legend = FALSE)+
				          scale_x_continuous(breaks=c(1,2,3,4), labels=c("January", "February", "March", "April"))+
				              labs( x = 'Data', y = 'probability',title = 'Sample1')
p
```

![plot_broken_line5](/images/posts/R/plot_broken_line5.png)


### 参考资料

* [ggplot2绘图入门](http://www.plob.org/2012/09/20/3553.html)
* [使用ggplot2画图](http://www.plob.org/2014/05/11/7264.html)
* [ggplot2——坐标系篇](http://www.2cto.com/kf/201508/431434.html)