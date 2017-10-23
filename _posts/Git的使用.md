---
title: Git的使用
date: 2015-12-29 10:19:14
tags: Git
categories: Git
---

# 各种命令

## 1.配置用户名
**注：三个级别：system系统的、global针对当前用户全局的、local当前仓库**
**①增加   git config --global user.name xxxxxx**
**②增加用户名  git config --global --add user.name xxxx**
**③删除用户名  git config --global --unset user.name xxxxxx**
**④查询   git config --list --global**
**⑤修改  git config —global user.name xxxx**

## 2.初始化Git仓库
**初始化： git init ，然后将本地项目push到远程仓库。或者  git clone url 将远程仓库代码克隆下来。**

<font color="#4590a3">注：pwd 显示当前目录。</font>


## 3.提交文件
**①添加文件到本地暂存区 ： git add 文件名。  git add . 或者  git add -A 提交所有文件到暂存区。**
**②提交到本地历史记录：git commit -m ‘提示’**
**③推送到远程仓库：git push origin master**




## 4.撤销修改
**①从暂存区撤出 ： git reset 文件名。  git reset .从暂存区恢复所有add。**
**②丢弃工作区的修改：git checkout --readme.txt**
**③回滚到某个commit：git reset --hard 版本号。 可以用git log查询版本号。**
**④删除某个文件：git rm xxx   (把工作区的文件和暂存区的引用同时删除掉)  git rm --cached xxx    (只删除暂存区的文件)**



## 5.分支
**①创建分支   git branch test**
**②切换分支   git checkout test**
**③删除分支   git branch -d test**

## 6.更新

**git fetch：相当于是从远程获取最新版本到本地，不会自动merge    例：git fetch origin master**
** git pull：相当于是从远程获取最新版本并merge到本地   例：git pull origin master**