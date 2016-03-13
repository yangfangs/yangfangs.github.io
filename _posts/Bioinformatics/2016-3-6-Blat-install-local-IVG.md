---
layout: post
title: Blat本地安装使用以及结果查看
categories: bioinformatics
tags:
description: 本地blat的用法
keywords: 生物信息学, blat
---

# Blat本地安装使用以及结果查看

*  在进行NGS结果分析的时候，很多时候我们向快速查看一下从测序公司得的测序文件，这里有一个比较好的查看工具

　　就是[Blat](https://genome.ucsc.edu/cgi-bin/hgBlat?org=human)当然你可以使用在线版本的快速查看，有时候在线版本并没有涵盖你分析物种的基因组，就不得不使用本地版本，

　　这里介绍下本地版本blat的使用。

## Blat的本地版本的安装

* 首先现在下载去UCSC网站下载[Blat](https://genome.ucsc.edu/FAQ/FAQblat.html#blat3)下载到本地是一个zip压缩文件blatSrc.zip
* 执行命令`unzip blatSrc.zip`解压文件，解压后不能直接安装需要配置一下
* 配置安装blat：我的在Linux下进行的，在终端依次输入
* `MACHTYPE=i686`　　//在这里如果是32位操作系统的话就改为i386
* `export MACHTYPE`　　//导入本地
* `chmod +x ~/bin/$MACHTYPE`  //确保这个文件可执行
* `vim ~/.bashrc` 复制这条命令`export PATH="$PATH:/home/yangfang/bin/i686"`
到bashrc中
* 然后进入blat文件夹下的lab文件夹下查看又没有i686这个文件夹，若没有终端执行`mkdir $MACHTYPE`创建
* 切断到blatSrc目录终端执行`make`就安装成功了

## Blat的使用

* 由于blat加入了环境变量，所以终端的任何目录就可以执行blat命令了
* 下面是一个典型的RNA-seq使用blat快速map的方法
* `blat GCF.fa test_R1.fasta output.psl -q=rnax -t=dnax` //其中`GCF.fa`是参考基因组,

　　`test_R1.fasta`是标准的fasta格式文件`output.psl`是输出map的结果,

　　`-q`和`-t`是相应的参数，具体参数说明可以查看[UCSC](https://genome.ucsc.edu/goldenPath/help/blatSpec.html#blatUsage)关于参数的说明

## Blat结果查看

* 查看`.psl`文件可以使用[IGV](https://www.broadinstitute.org/software/igv/download)软件来查看
* 下载后执行 `unzip IGV_2.3.68.zip`　解压
* 然后到解压目录执行`java -Xmx750m -jar igv.jar`就可以使用本地IGV来查看`.psl`格式文件的结果了
