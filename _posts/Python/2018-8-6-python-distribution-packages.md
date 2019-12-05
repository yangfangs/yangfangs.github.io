---
layout: post
title: Python 快速打包发布软件PyPi上
categories: Python
description: Python　打包　distribution package 发布
keywords: python3, distribution, 发布
---

  [PyPi](https://pypi.org/)是一个python包的仓库，就如 R 的[CRAN](https://cran.r-project.org/mirror-howto.html)和 perl 的[CPAN](https://www.perl.org/cpan.html)一样，里面有很多别人打包发布的python包，你可以通过easy_install或者pip进行安装,方便用户更方面的使用你的代码模块。
本文记录了如何创建自己的 Python 包,以及打包发布到PyPi上。

# 首先安装打包必要的工具

* 打包必须依赖工具

```bash
sudo pip install setuptools
```
* 方便上传工具

```bash
sudo pip install twine
```


# 在[PyPi](https://pypi.org/)官网注册一个PyPi个人账户如下

![PyPi](/images/posts/Python/PyPI_Index.png)


# 配置本地打包配置文件`setup.py`

```python
from setuptools import setup, find_packages

from version.version import VERSION

GFICLEE_VERSION = VERSION

setup(
    name='GFICLEE',
    version=GFICLEE_VERSION,
    packages=find_packages(),
    entry_points={
        "console_scripts": ['GFICLEE = predict.main:main']
    },
    install_requires=[
        "numpy==1.14.3",
        "pandas==0.22.0",
    ],
    url='https://github.com/yangfangs/GFICLEE',
    license='GNU General Public License v3.0',
    author='Yang　Fang',
    author_email='yangfangscu@gmail.com',
    description='Gene function inferred by common loss evolution events'
)
```
* 这些是打包必要的说明对应如下：

|  名称 |  说明 |
|---|---|
|  name |  项目名称 |
| version  |  项目版本 |
|  packages |  项目包含的数据 |
|  entry_points |  项目的主入口 |
|  install_requires |  项目依赖包 |
|  url |  项目地址 |
|  author | 项目作者  |
|  author_email | 作者邮箱  |
|  description | 项目简要描述  |


> 注： 项目版本一般不直接写入`setup.py`中,一般另写其他Python脚本中然后导入，便于统一管理和发布新版本。
> `packages`可以使用 `find_packages()`函数实习本项目内自动寻找。


# 打包


* 打包前可以先check一下

```bash

python setup.py check

```
* 执行打包命令

```python

python setup.py sdist

```
> 打包完成会生成相应的文件保存在 `dist/`目录下 名为`tar.gz`结尾文件

# 发布Python 包

1.在Home新建一个隐藏文件名为`.pypirc`，写入PyPi账户以及密码信息，这样每次上传不需要再繁琐的输入用户名和密码了。


```bash
[distutils]
index-servers =
    pypi

[pypi]
username:your_username
password:your_password

```

2.本地测试

```bash
python setup.py install
```

3.注册包

* 上传前需要注册一下包的名称，因为这个名称必须独一无二，如被占用则注册不通过。

```bash
python setup.py register
```
4.检测是否符合Pypi要求

```bash

twine check dist/**_.tar.gz

```

5.上传

```bash
twine upload dist/**_.tar.gz
```

完成上传你就可以在Pypi上看到你上传的包了。并且可以使用`pip install`安装你的包了。