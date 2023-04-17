---
title: gitlocal2online
typora-root-url: gitlocal2online
tags: 学习经验
abbrlink: 5ede5840
date: 2023-03-19 22:48:10
categories:
---


### 介绍一下git仓库的代码管理功能





一、**首先去github创建一个仓库**

![image-1](/images/papers/gitlocal2online/image-1.png)





**注意**在新建仓库时 请不要在创建Initialize this repository with a README前打勾，`Add .gitignore`和`Add a license`处请选择None。







**二、**本地相关设置

我这里建立一个rcnn文件夹 并在里面放了一个test文件  在此文件夹下打开终端，运行

```text
$ git init  
```

此时，我们仅作了一个初始化的操作，你的项目文件还未被跟踪。

![image-20230319213026846](/images/papers/gitlocal2online/image-20230319213026846.png)

![image-20230319213216823](/images/papers/gitlocal2online/image-20230319213216823.png)



通过git add 来实现对指定文件的跟踪，然后执行git commit提交:



```text
$ git add .
$ git commit -m "initial commit"
```

设置 username 和 email

```text
$ git config --global user.name "your name"
$ git config --global user.email "your_email@youremail.com"
```







首先在本地创建 ssh key：           ssh-keygen -t rsa -C "your_email@youremail.com"

会在home/用户名/.ssh文件夹下生成如下文件， 需要输入三个  回车 

![image-20230319221741516](/images/papers/gitlocal2online/image-20230319221741516.png)









回到之前我们创建GitHub仓库完成的页面，复制远程仓库链接，在终端输入:

```text
$ git remote add origin <远程仓库链接>
```



你可以通过`git remote -v`来验证你的链接是否正确。

验证完毕，确认准确无误后，用以下指令推送本地仓库内容至GitHub





第一次使用git时
$ git push -u origin master

此时还会提示要 .ssh文件夹缺少一个文件,输入yes即可 自动生成相关的文件

第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。



之后使用git 时候  就直接  用   $ git push origin master























最终的效果就是下面这张图

![image-20230319221610783](/images/papers/gitlocal2online/image-20230319221610783.png)