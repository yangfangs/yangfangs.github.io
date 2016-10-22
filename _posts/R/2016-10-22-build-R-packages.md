---
layout: post
title: "Hello World"为例创建R包
categories: R
description: R语言打包
keywords: packages, R, create
---

　　这里给出了两种非常简单的方法来创建R包，Fedora 24 开发版下测试成功。

# 直接Linux 命令行下创建R包

## 写一个R脚本

　　这里有一个R脚本包含一个`HelloWorld`函数存放在 `HelloWorld.R`　中

```r
$ cat /home/yangfang/testRpackage/R/HelloWorld.R

HelloWorld <- function(name){
  print(paste("Hello World, ",name))
}
```

## 创建R包开发的基本结构

```bash
# 启动R
$ R

#清空所以内载入变量
> rm(list=ls())
#check下
> ls()
character(0)
#改变工作目录
> setwd("/home/yangfang/testRpackage/R/")
#创建基本打包目录结构
> package.skeleton(name="HelloWorld",code_files="/home/yangfang/testRpackage/R/HelloWorld.R")

```

## 目录结构说明

HelloWorld (包的名字)
|
|--DESCRIPTION (描述文件，包括包名、版本号、标题、描述、依赖关系等)
|--NAMESPACE (包的命名空间文件)
|--R (函数源码)
   |--HelloWorld.R
   |--...
|--man (帮助文档，存放函数说明文件的目录)
   |--HelloWorld.Rd (函数的说明文件，latex语法，用来生成PDF文档)
   |--HelloWorld-package.Rd (包的说明文件，可以删除)
|--Read-and-delete-me 说明文件,已经说的很清楚了，读一读就把我删除了吧

## 编辑DESCRIPTION文件

```
Package: HelloWorld
Type: Package
Title: a example of HelloWorld
Version: 1.0
Date: 2016-10-21
Author: Yang Fang
Maintainer: Yang Fang <yangfangscu@gmail.com>
Description: a example of create R Package
License: GPL
```

## 编辑HelloWorld.Rd文件

```
\name{HelloWorld}
\alias{HelloWorld}

\title{
a HelloWorld function
}
\description{
a HelloWorld function
}
\usage{
HelloWorld(name)
}
\arguments{
  \item{name}{
your name
}
}
\details{
NULL
}
\value{
not have return
}
\references{
NULL
}
\author{
Yang Fang
}
\note{
NULL
}
\seealso{
NULL
}
\examples{
HelloWorld("Yang Fang")
}
\keyword{ HelloWorld }
```

## 删除文件

```bash
$ rm HelloWorld/Read-and-delete-me 
$ rm HelloWorld/man/HelloWorld-package.Rd 
```


## 创建R包

```bash
$ R CMD build HelloWorld
* checking for file ‘HelloWorld/DESCRIPTION’ ... OK
* preparing ‘HelloWorld’:
* checking DESCRIPTION meta-information ... OK
* checking for LF line-endings in source and make files
* checking for empty or unneeded directories
* building ‘HelloWorld_1.0.tar.gz’

```

## 安装测试

```
$ R CMD INSTALL HelloWorld_1.0.tar.gz 
* installing to library ‘/home/yangfang/R/x86_64-redhat-linux-gnu-library/3.3’
* installing *source* package ‘HelloWorld’ ...
** R
** preparing package for lazy loading
** help
*** installing help indices
  converting help for package ‘HelloWorld’
    finding HTML links ... done
    HelloWorld                              html  
** building package indices
** testing if installed package can be loaded
* DONE (HelloWorld)
```

## 测试使用

```r
$ R
> library(HelloWorld)
> HelloWorld("Hi")
[1] "Hello World, Hi"

```

## check通过后发布

* 只有通过check的检查没有错误的包才能通过CRAN发布

```bash
$ R CMD check HelloWorld_1.0.tar.gz 
* using log directory ‘/home/yangfang/testRpackage/R/HelloWorld.Rcheck’
* using R version 3.3.1 (2016-06-21)
* using platform: x86_64-redhat-linux-gnu (64-bit)
* using session charset: UTF-8
* checking for file ‘HelloWorld/DESCRIPTION’ ... OK
* checking extension type ... Package
* this is package ‘HelloWorld’ version ‘1.0’
* checking package namespace information ... OK
* checking package dependencies ... OK
* checking if this is a source package ... OK
* checking if there is a namespace ... OK
* checking for executable files ... OK
* checking for hidden files and directories ... OK
* checking for portable file names ... OK
* checking for sufficient/correct file permissions ... OK
* checking whether package ‘HelloWorld’ can be installed ... OK
* checking installed package size ... OK
* checking package directory ... OK
* checking DESCRIPTION meta-information ... NOTE
Malformed Description field: should contain one or more complete sentences.
* checking top-level files ... OK
* checking for left-over files ... OK
* checking index information ... OK
* checking package subdirectories ... OK
* checking R files for non-ASCII characters ... OK
* checking R files for syntax errors ... OK
* checking whether the package can be loaded ... OK
* checking whether the package can be loaded with stated dependencies ... OK
* checking whether the package can be unloaded cleanly ... OK
* checking whether the namespace can be loaded with stated dependencies ... OK
* checking whether the namespace can be unloaded cleanly ... OK
* checking loading without being on the library search path ... OK
* checking dependencies in R code ... OK
* checking S3 generic/method consistency ... OK
* checking replacement functions ... OK
* checking foreign function calls ... OK
* checking R code for possible problems ... OK
* checking Rd files ... OK
* checking Rd metadata ... OK
* checking Rd cross-references ... OK
* checking for missing documentation entries ... OK
* checking for code/documentation mismatches ... OK
* checking Rd \usage sections ... OK
* checking Rd contents ... OK
* checking for unstated dependencies in examples ... OK
* checking examples ... OK
* checking PDF version of manual ... OK
* DONE

Status: 1 NOTE
See
  ‘/home/yangfang/testRpackage/R/HelloWorld.Rcheck/00check.log’
for details.
```

## 卸载测试的R包

```r
> remove.packages("HelloWorld")

```


# 使用Rstudio创建R包

* 一个专门可是化的IDE使创建R包变得更加的简便　[Rstudio](https://www.rstudio.com/) 就是这么一款IDE

## 创建R包

*依次点击 File--->New Project--->New Directory--->R Package

![Create R Package](/images/posts/R/create_R_package.png))


