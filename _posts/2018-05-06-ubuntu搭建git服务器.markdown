---
layout:     post
title:      "你好 2018"
subtitle:   "你好 YJM"
date:       2018-05-06 23:00:00
author:     "Cui Yan"
header-img: "img/2018-life.jpg"
catalog: true
tags:
    - 笔记
    - git
---

## 1.安装git

> `sudo apt install git`

## 2.创建git用户

> `sudo adduser git`

## 3.创建证书文件

收集所有需要登录的用户的公钥，公钥位于id_rsa.pub文件中，把我们的公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

如果没有该文件创建它：

> `cd /home/git
	mkdir .ssh
	chmod 700 .ssh
	touch .ssh/authorized_keys
	chmod 600 .ssh/authorized_keys
`

*用户公钥生成方法 在客户端电脑，cmd里输入 $ ssh-keygen -t rsa -C "youremail@example.com"*
*把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可*
*在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH*
*Key的秘钥对，id_rsa是私钥，id_rsa.pub是公钥*

## 4.初始化git仓库

首先我们选定一个目录作为Git仓库，假定是/home/intelligent_doctor.git，输入命令：

> `cd /home/git
	git init --bare intelligent_doctor.git
`

以上命令Git创建一个空仓库，服务器上的Git仓库通常都以.git结尾。然后，把仓库所属用户改为git：

> `chown -R git:git intelligent_doctor.git`

## 5.禁用shell登录

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

git:x:1001:1001:,,,:/home/git:/bin/bash

改为：

git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

## 6.克隆远程仓库

现在，可以通过git clone命令克隆远程仓库了，在客户端的电脑上运行：


> `git clone git@192.168.2.9:/home/git/intelligent_doctor.git`


**原文地址** 点击[这里](https://www.cnblogs.com/qq413572713/p/7122743.html)
