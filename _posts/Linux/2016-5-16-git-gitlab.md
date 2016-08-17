---
layout: post
title: gitlab 创建与 git 的使用
categories: Linux
description: 使用git
keywords: gitlab, git
---

　　[git](https://git-scm.com/) 可以这么理解，就相当于本地的一个软件，这个软件是干什么用的呢？就是在本地对代码进行分布式管理，而 [github](https://github.com/)　和 [gitlab](https://gitlab.com/),就是一个远程的仓库，就像云盘一样，保证当你电脑熄火了，你的代码依然存在（远程仓库上）, github 与　gitlab 的区别，对我而言比较有价值的是，gitlab　提供了免费的私人库的创建，这已经很爽了．





# 1.注册账户


* 在 [github](https://github.com/) 官网上先注册一个账户 


# 2.本地配置git

* 为了避免麻烦每次 push　代码都要输入账户名称和密码，我们需要再本地与远程仓库建立一个通信协议， ssh 协议


## 生成 sshkey

```bash
ssh-keygen -t rsa -C "$you@eamil"


```
* 在这里生成秘钥是有一对儿的，正好作为通信的信物，一个私钥放在了 `~/.ssh/id_rsa`　和一个公钥放在了 `~/.ssh/id_rsa_pub`



## 把公钥配置的远程仓库上(github或gitlab) 

* 登陆　gitlab　依次点击Profile Settings –> SSH Keys –> Add SSH Keys, 把cat　拷贝过来保存就好了

```bash
cat ~/.ssh/id_rsa.pub

```


## gitlab 上创建一个远程仓库


* 点击 `New project`　创建一个远程仓库，依次键入工程名字，说明，以及开放级别，我做私人仓库用一般选第一个

![create project](/images/posts/Linux/gitlab.com-.jpg)




## 本地代码同步远程


![add_project](/images/posts/Linux/gitlab.com-add-project.jpg)


* 首先在本地配置下全局的　git 信息配置　--global　的意思是你的所有工程上传时候都用这一个信息

```bash
git config --global user.name "you name"
git config --global user.email "you@email"

```

* 然后两种方式来同步，第一种：直接克隆你创建的仓库到本地．


```bash
git clone git@gitlab.com:xiaoxiaoyang/project.git
cd project
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master

```

* 第二种是：扩展本地的仓库直接到你gitlab上新创建的仓库


```bash
cd existing_folder
git init
git remote add origin git@gitlab.com:xiaoxiaoyang/project.git
git add .
git commit
git push -u origin master

```

* 到此本地代码同步到远程已经完成了



# 3.git基本使用

## 本地提交代码到远程仓库

* 添加本地变动到本地仓库


```bash
git　add .

```

* 查看变动状态


```bash

git status

```


* 添加变动说明

```bash
git commit -m "update code"

```

* 推送到远程仓库（主分支）

```bash
git push origin master

```

## 更新远程仓库代码到本地


```bash

git pull origin master
```

## 本地创建分支进行开发

* 本地创建一个叫做 dev 的分支

```bash
git checkout -b dev

```

* 查看所处的分支（*表示现在所在的分支）

```bash

git branch

```

* 切换到 dev 进行分支开发

```bash
git checkout dev 

```

* 开发完后觉得很不错，就可以合并到主分支了

```bash
git checkout master
git merge dev
```

*　合并前可以看看分支与主分支的不同

```bash
git diff dev

```

* 分支已经完成他的工作了也活到头了可以删除之

```
git branch -d test 
```

*有时候你想要删除的分支还没合并到其他分支去的画，就不能直接删除需要强制删除，使用 `git branch -D`

## 本地分支在远程保存一份

* 切换到分支

```bash

git checkout dev
```

* 添加分支内容到远程仓库

```bash
git add .
git commit -m "add dev branch"
git push origin dev

```

## 删除远程分支

* 查看所有分支,找到想要删除的远程分支

```bash
git branch -a

```

* 推送一个空分支(空格表示)到相应的远程分支，就等于删除


```bash
git push origin :dev

```

## 添加tag方法

* 添加一个tag在本地

```bash

git tag -a v0.0.3 -m 'version 0.0.3'
```

* push到远程仓库

```bash
git push origin --tags

```

## 删除tag方法

* 查看tag


```bash

git tag
```

* 删除本地tag

```bash
git tag -d tagname

```

* 删除远程仓库tag

```bash
git push origin :refs/tags/tagname

```


## 忽略上传文件方法


* 再根目录建立一个隐藏文件 `.gitignore`加入想要忽略的文件或目录

```bash
mkdir .gitignore
vim .gitignore
```
* python　开发常忽略文件

```
#git ingore files use python developed
# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build
```

## 修改本地对应远程仓库地址


```bash
git remote set-url origin　[newurl]

git push -u origin master

```



# 4. `gitignore` 中加入文件为什么没有被忽略？

* 没有被忽略的原因是你在把文件加入 `gitignore` 之前，git 仓库就已经跟踪(track)这个文件了，所以在这只有加入这个文件是不起作用的，需要再git版本控制中移除对这个文件的track就行了

* 解决办法一:直接移除对这个文件的跟踪

```bash
git rm --cached [filename(s)]

```

* 解决办法二:直接再git本地仓库删除这个文件

```bash
git rm [filename(s)]

```

* 解决办法三:让git不去检查这个文件的变化

```bash

git update-index --assume-unchanged [filename(s)]
```












