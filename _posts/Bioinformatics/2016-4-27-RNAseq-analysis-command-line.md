---
layout: post
title: 分析生物数据 bash 命令
categories: bioinformatics
description: bash 命令
keywords: 生物信息学, bash, 命令行
---

　　进行二代测序结果分析时候，对文件的操作有时候直接用 bash 下命令行简易编程是很方便的，例如使用 sed　和 awk　命令来操作文件．

# 统计文件有多少行

* 可以直接使用 `wc -l`

```bash

wc -l file.fastq

```

* 如果是 `zip` 压缩文件可以使用命令 `gunzip`

```bash
gunzip -c file.gz | wc -l

```
* 或者使用 awk 命令

```
awk 'END{print NR}'
```

* bash 中使用数学计算

```bash
echo $((40/4))

```



# 合并文件


```bash
cat file1.gz file2.gz file3.gz > allfiles.gz

```


# gff3文件转换为 gtf 文件

* 可以利用 cufflinks　提供的工具 gffread

```bash
gffread file.gff3 -T -o file.gtf

```

# awk 处理　gff 文件

* 删除第三列中含有 "reaion" 和　"sequence_variant" 的行，并删除注释行

```bash

awk -F '\t'  '$3 != "region" && $3 != "sequence_variant"' file.gff | grep -v "#" > file_update.gff

```


# 替换关键字


```bash
sed's/GeneID/Gene_ID/g' file.gff > file2.gff

```

# 提取某一列

* 在这里提取以tab分割分隔符数据的第一列

```bash
awk -F '\t' '{print $1}' filename.txt > outputfilename.txt

```


# 条件筛选

* 筛选第二列小于等于５的条件值

```bash
awk '$2 <=5 {print }' out_R1.psl　> out_R2.psl

```


# 删除行

* 删除首行

```bash
sed '1d' file.txt

```

* 删除尾行

```bash

sed '$d' file.txt

```

* 删除第３行至末尾

```bash
sed '2,$d' file.txt

```

* 删除文件中所有包含 GeneID 的行

```bash
sed '/GeneID/d' file.txt

```

* 保留所有包含 GeneID 的行

```bash
sed '/GeneID/!d' file.txt
```

* 删除文件中所有的空行

```bash
sed '/^$/d' file.txt

```


# 使用awk为每一行行头添加数据

```bash
awk '{print "w "$0}' file.txt

```

# 指定输入和输出的分隔符

* `-F` 指定输入分隔符， `-vOFS` 指定输出分隔符

```bash
awk -F '\t' -vOFS="\t" '{print $2,$1}' file1 > file2

```

# 数据加上head标题

* 使用 `'BEGIN{print""}'`

```bash
awk 'BEGIN{ print "Symbol\tGene set name" }{print}' file1 > file2

```

# 统计当前目录下文件个数

* 统计文件个数

```bash
ls -l |grep "^-"|wc -l
```

* 统计目录个数

```bash
ls -l |grep "^d"|wc -l
```

* 统计包括子文件夹下文件个数

```bash
ls -lR|grep "^-"|wc -l
```

* 统计包括子目录目录个数

```bash
ls -lR|grep "^d"|wc -l
```

# grep

* `grep` 带分隔符的数据(以Tab为例)

```
grep 'B8BUD4'$'\t''A7RKS9' file.txt

```


***

**2019.7.25更新**

***






















