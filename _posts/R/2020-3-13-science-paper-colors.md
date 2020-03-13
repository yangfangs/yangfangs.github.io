---
layout: post
title: 科研彩图常用的配色方案-ColorBrewer的使用
categories: R
description: 科研图片配色，彩图，出版
keywords: colors, science, always used
---

  前段时间师兄推荐一个科研图常用配色系统[Colorbrewer][1]非常不错，好的彩图配色方案能增加你文章的整体的观感，更容易让人接受能。好的彩色配色方案应该具有高的区分度，
能让人一眼能分清 legend 展示和相对应图中各个曲线或者柱状图。后来发现到 ggplot2 和 Adobe illustrator 中都有相应的调色版非常方便，记录下使用方法。

# 1 使用Colorbrewer网站获取颜色

## Colorbrewer2.0网站

![Colorbrewer](/images/posts/R/ColorBrewer_Color.png)

## Colorbrewer2.0使用说明

* sequential: 连续型单渐变色，色彩由一种颜色并且从浅到深排列。这种色彩组合适用于连续型数据展示。
* diverging: 离散型双渐变色，色彩由一种到另一种颜色的高区度排列。这种色彩组合适用于离散数据的展示。
* qualitative: 高区分度色。色彩由区分度极高的颜色组成。这种颜色适用于高区分度曲线或者柱状图使用。
* Colorbrewer2.0 最多提供12种颜色组合,基本能应付所有画图组合。
* Colorbrewer2.0 提供的十六进制的色彩代码例如 `#762a83` 和 `#5aae61`




# 2 使用 R 语言的 [RColorBrewer][2]包提供的色彩方案

# 使用 `display.brewer.all()` 查看 RColorBrewer 包的调色版

```R
> library(RColorBrewer)
> display.brewer.all()
```
![Colorbrewer](/images/posts/R/ColorBrewer_Color.png)


## 使用`brewer.pal.info` 命令查看色彩系统。

```R
> brewer.pal.info
         maxcolors category colorblind
BrBG            11      div       TRUE
PiYG            11      div       TRUE
PRGn            11      div       TRUE
PuOr            11      div       TRUE
RdBu            11      div       TRUE
RdGy            11      div      FALSE
RdYlBu          11      div       TRUE
RdYlGn          11      div      FALSE
Spectral        11      div      FALSE
Accent           8     qual      FALSE
Dark2            8     qual       TRUE
Paired          12     qual       TRUE
Pastel1          9     qual      FALSE
Pastel2          8     qual      FALSE
Set1             9     qual      FALSE
Set2             8     qual       TRUE
Set3            12     qual      FALSE
Blues            9      seq       TRUE
BuGn             9      seq       TRUE
BuPu             9      seq       TRUE
GnBu             9      seq       TRUE
Greens           9      seq       TRUE
Greys            9      seq       TRUE
Oranges          9      seq       TRUE
OrRd             9      seq       TRUE
PuBu             9      seq       TRUE
PuBuGn           9      seq       TRUE
PuRd             9      seq       TRUE
Purples          9      seq       TRUE
RdPu             9      seq       TRUE
Reds             9      seq       TRUE
YlGn             9      seq       TRUE
YlGnBu           9      seq       TRUE
YlOrBr           9      seq       TRUE
YlOrRd           9      seq       TRUE

```
* 从上到下依次是 diverging, qualitative, sequential 分类以及每类颜色个个数。

# 使用 `display.brewer.pal()` 查看具体每个配色方案
```R
display.brewer.pal(8,"Set1") 
```

![colorbrewer_package](/images/posts/R/colorbrewer_package_each_color.png)

# 使用 ` brewer.pal(8,"Set1")` 获取十六进制颜色代码

```R
 > brewer.pal(8,"Set1")
 [1] "#E41A1C" "#377EB8" "#4DAF4A" "#984EA3" "#FF7F00" "#FFFF33" "#A65628" "#F781BF"
```

# 使用`colorRampPalette()`自定义颜色个数

```R
cols<-brewer.pal(8, "YlGnBu")
pal<-colorRampPalette(cols)
mycolors<-pal(20)
image(1 : length(mycolors), 1, as.matrix(1 : length(mycolors)), col = mycolors ,xlab =  "", ylab = "", xaxt = "n", yaxt = "n", bty = "n")
```

![colorRampPalette_self.png](/images/posts/R/colorRampPalette_self.png)


# Adobe Illustrator 中使用ColorBrewer调色版

* AI中直接配有科学色彩库方便科学用色，依次菜单窗口--->色板--->色板库--->科学,选择需要的颜色。


![AI_color.png](/images/posts/R/AI_color.png)




# 参考

[Exploratory Data Analysis with R][3]
[使用 ggplot2 和 RColorBrewer 扩展调色板][4]
[RColorBrewer与ggplot2][5]

[1]: https://colorbrewer2.org/
[2]: https://cran.r-project.org/web/packages/RColorBrewer/index.html
[3]: https://bookdown.org/rdpeng/exdata/plotting-and-color-in-r.html
[4]: https://www.cnblogs.com/shaocf/p/9600340.html
[5]: https://www.jianshu.com/p/a8856757a0d2