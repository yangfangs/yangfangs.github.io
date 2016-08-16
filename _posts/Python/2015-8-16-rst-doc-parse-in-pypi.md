---
layout: post
title: README.rst文档在PyPi中无法解析解决办法
categories: Python
description: README.rst Parse
keywords: PyPi, reStructuredText, README.rst, Parse
---

　　一个README.rst说明文档在github上解析是正常的，上传的PyPi中却完全不能解析，原样展示。这绝对不能忍啊，找找原因，发现原来不能解析是由于
github和PyPi对reStructuredText文档解析工具的版本不同，PyPi使用的是0.8版本，而github使用的是 0.9或者0.10了，所有PyPi对文档要求很严格，
语法错误是导致不能解析的主要原因。

　　查找解决办法就是查看文档哪里的语法不对，当然文档太长自己也发现不了，直接肉眼看是不可能了，只有借助工具了，[collective.checkdocs](https://github.com/collective/collective.checkdocs)工具是个不错的选择。


# 安装 collective.checkdocs

```bash
$pip install collective.checkdocs

```

# 检测文档

```bash
$python setup.py checkdocs
```

# 反馈结果的分析

```bash
python setup.py checkdocs
/home/yangfang/lib/python2.7/site-packages/setuptools-20.7.0-py2.7.egg/setuptools/dist.py:285: UserWarning: Normalizing 'v0.1.6' to '0.1.6'
running checkdocs
<string>:67: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:73: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:83: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:89: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:93: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:97: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:111: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:159: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:209: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:216: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:241: (WARNING/2) Cannot analyze code. Pygments package not found.
<string>:281: (WARNING/2) Inline emphasis start-string without end-string.
<string>:287: (WARNING/2) Inline emphasis start-string without end-string.
<string>:287: (WARNING/2) Inline emphasis start-string without end-string.
<string>:287: (WARNING/2) Inline emphasis start-string without end-string.
<string>:288: (WARNING/2) Bullet list ends without a blank line; unexpected unindent.
<string>:288: (WARNING/2) Inline emphasis start-string without end-string.
<string>:294: (WARNING/2) Title underline too short.

```

* `UserWaring:` 是在说软件的版本信息写的不对，在 setup.py 中应该写 version = '0.1.6' 而不是　version = 'v0.1.6'。（呵，挺智能啊这都能检测到）
* `Cannot analyze code. Pygments package not found.` 是在告诉我们 `Pygments`包没有安装，无法分析代码块部分的书写是否正确。
* `Inline emphasis start-string without end-string.` 是在说我的文档中第281、287等行以 \*开头的加粗强调只有开头没有结尾（没有成对出现），在这里我是想用\*号的而不是强调，需加反斜杠来转意就好了。
* `Bullet list ends without a blank line; unexpected unindent` 告诉我的文档第288行的首行缩进有问题，没有对齐。
* `Title underline too short.` 是说我的文档第294行的标题，下划线居然敢比标题还短，真够省事的。

# 修正文档

1. 修改文档中的语法错误

2. 安装个　[Pygments](https://pypi.python.org/pypi/Pygments) 检测下代码块语法有没又错误

```bash
$pip install Pygments
Collecting Pygments
  Downloading Pygments-2.1.3-py2.py3-none-any.whl (755kB)
    100% |████████████████████████████████| 757kB 1.2MB/s
Installing collected packages: Pygments
Successfully installed Pygments-2.1.3
```

3. 再次测试

```bash
$python setup.py checkdocs
running checkdocs
```
* 没有`WARING`表示全部通过了。

4.　更新上传至`PyPi`的发布版本，在开发包的主页面`README.rst`文档已经可以成功的解析了。


参考：

* [stackoverflow: "reStructuredText: README.rst not parsing on PyPI" ](http://stackoverflow.com/questions/17401132/restructuredtext-readme-rst-not-parsing-on-pypi)