---
layout: post
title: 分析生物数据　bash　命令
categories: bioinformatics
description: bash 命令
keywords: 生物信息学, bash, 命令行
---

　　进行二代测序结果分析时候，对文件的操作有时候直接用 bash 下命令行简易编程是很方便的，例如使用 sed　和 awk　命令来操作文件．

# 统计文件有多少行


```bash

wc -l file.fastq

```

* 如果是压缩文件可以使用命令

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






























