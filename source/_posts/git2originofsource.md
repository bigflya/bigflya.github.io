---
title: 通过master 和source 两个分支来管理自己的博客
typora-root-url: git2originofsource
tags: git
abbrlink: 3699c3ab
date: 2023-04-15 12:58:24
categories:
---



这里主要介绍一下通过master 和source 两个分支来管理自己的博客。 



分支有 master   

和    source  （默认）





master 分支用来存放个人的博客部署文件  ，source用来存放个人的博客源文件



对于master 分支的  上传及更新 请参考另外一篇 博客 ，这里主要说一下关于source分支的设置过程。







3、 git remote add origin https://github.com/bigflya/bigflya.github.io.git

![image-20230415123804472](/images/papers/git2originofsource/image-20230415123804472.png)

若报错如上 执行       git remote rm origin



4、git add .

5、 git commit -m 'hexo source files'

6、 git push origin source

![image-20230415123920689](/images/papers/git2originofsource/image-20230415123920689.png)



git branch -m source

若报错如下图可执行步骤7


![image-20230415130345452.png](/images/papers/git2originofsource/image-20230415130345452.png)

7、获取token  并绑定此仓库

之后用自己生成的token登录，把上面生成的token粘贴到输入密码的位置，然后成功push代码！

也可以 把token直接添加远程仓库链接中，这样就可以避免同一个仓库每次提交代码都要输入token了：

git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git

<your_token>：换成你自己得到的token
<USERNAME>：是你自己github的用户名
<REPO>：是你的仓库名称

token 的获取可以点击[传送门]()参考我的另一篇文章。







git remote set-url origin https://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@github.com/bigflya/bigflya.github.io.git

8、上传source 分支       git push origin source

这里如果报错直接强行上传命令如下：

 git push origin +source







拉取 远程源文件 流程 



  git clone https://github.com/bigflya/bigflya.github.io

每次提交流程

二、提交代码

1、git add .（添加文件到暂存区）
2、git commit -m "提交描述信息"（提交暂存区到本地仓库）
3、git push origin source（上传远程代码并合并



参考



[(19条消息) Git时出现“error: 源引用表达式 main 没有匹配 error: 推送一些引用到 ‘https://github.com/***.git‘ 失败”的错误提示_源引用规格 main 没有匹配_songyuc的博客-CSDN博客](https://blog.csdn.net/songyuc/article/details/115251254)



[使用git分支保存hexo博客源码到github | 小冰的个人博客 (yangbing.club)](https://www.yangbing.club/2019/06/29/save-hexo-source-post-with-git-branch/)



[(19条消息) git问题error: remote origin already exists._myydan的博客-CSDN博客](https://blog.csdn.net/myydan/article/details/129259615?ops_request_misc=%7B%22request%5Fid%22%3A%22168061482516800192217379%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=168061482516800192217379&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-129259615-null-null.142^v81^insert_down1,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=error%3A 远程 origin 已经存在。&spm=1018.2226.3001.4187)



[(19条消息) Git时出现“error: 源引用表达式 main 没有匹配 error: 推送一些引用到 ‘https://github.com/***.git‘ 失败”的错误提示_源引用规格 main 没有匹配_songyuc的博客-CSDN博客](https://blog.csdn.net/songyuc/article/details/115251254)



