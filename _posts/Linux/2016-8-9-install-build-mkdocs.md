---
layout: post
title: Mkdocs 配置和使用
categories: Linux
description: Mkdocs
keywords: Mkdocs, Linux, Markdown, documentation
---

  有时候我们在开发一个项目的时候想写一份友好的文档来帮助用户使用，这时候我们可以选择使用 [Mkdocs](http://www.mkdocs.org/) 来搭建一个友好而又很专业的文档，Mkdocs可以很好托管
在github上，使用 Mkdocs　会再你主项目下建一个gh-pages的分支，然后把你文档生成的静态site托管在上面，访问时候只需要访问`http://{username}.github.io/{projectname}`来访问
文档，文档全部使用　Mrakdown　语法来写很方便．

# 安装 Mkdocs

* Mkdocs是用Python开发的工具可以使用pip命令来安装

```bash
sudo pip install mkdocs

```

# 使用

* 使用很简单直接在命令行

```bash
mkdocs new my-project

```

这样就会在本地建立一个`my-project`文件夹　其中包括了一个`mkdocs.yml`和一个`docs`文件夹

* **mkdocs.yml**: 这个文件是一个配置文件主要配置你的站点名字，板块等[具体配置点我](http://www.mkdocs.org/user-guide/configuration/)
* **docs**: 是存放你要写的 Markdown 文档的地方初始化一个`index.md`[文档配置点我](http://www.mkdocs.org/user-guide/writing-your-docs/)

* 在本地查看搭建的文档效果

```bash
$ mkdocs serve
Running at: http://127.0.0.1:8000/

```

* 然后访问[http://127.0.0.1:8000/](http://127.0.0.1:8000/)就可以看到生成文档的效果了


# github上配置文档

* mkdocs　很友好的提供了一键托管github的命令'mkdocs gh-deploy --clean'来完成这一工作，当然你也可以手动完成．

* 完整的方法：到你正在开发的一个项目的目录下例如'my-progect'执行

```bash
mkdir docs
cd docs
mkdocs new .
mkdocs build
echo "site/" >> .gitignore
```
需要修改一下配置文件`mkdocs.yml`把site_name改成自己项目的名称例如修改成 `site_name:myproject`然后托管到github上

```bash
mkdocs gh-deploy --clean
```

然后就可以在你访问你的文档了地址`http://{username}.github.io/{projectname}`其中projectname就是你site_name的名字

# 常配置的一些项


## 增加页面

```bash
echo 'This is about me page'　> docs/about.md

```

在配置文件`mkdocs.yml`中配置增加的页面

```
site_name:myproject
pages:
- Home: index.md
- About: about.md
```

## 更改文档模板

修改配置文件`mkdocs.yml`中的`theme`值. [更多模板](http://www.mkdocs.org/user-guide/styling-your-docs/) 

```
site_name: MkLorum
pages:
- Home: index.md
- About: about.md
theme: readthedocs
```


# 参考：

[Mkdocs 官网](http://www.mkdocs.org/)





