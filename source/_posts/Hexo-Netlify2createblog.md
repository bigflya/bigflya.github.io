---
title: Hexo+Netlify搭建个人博客
typora-root-url: Hexo+Netlify2createblog
tags:
  - Hexo
  - Netlify
categories: 经验分享
abbrlink: c51939b6
date: 2023-01-13 09:22:53
---



系统环境：ubuntu22.04LTS(笔者采用的是在vmware16虚拟机里面装了ubuntu22.04LTS版本)

# 一、准备工作

1. 在ubuntu系统文件的home/用户名 目录下创建hexo 文件夹，并在hexo文件夹下面创建blog文件夹（我这里的用户名是：bigfly）


![图1](/images/papers/Hexo+Netlify2createblog/3.png)


2. 在hexo文件夹下面右击鼠标，打开终端

![图2](/images/papers/Hexo+Netlify2createblog/4.png)


3. 在终端中执行以下命令

   ```shell
   sudo su  #进入超级用户模式
   apt-get update 
   apt-get install git -y
   git clone https://github.com/creationix/nvm.git nvm #安装nvm
   source /home/bigfly/hexo/nvm/nvm.sh #注意将bigfly改为自己的用户名
   
   cat  /home/bigfly/hexo/nvm/nvm.sh >> ~/.bashrc
   source ~/.bashrc #添加环境变量
   
   nvm install node
   npm install -g hexo-cli #安装一些依赖
   ```

4. 所有准备已经完成可以查看一下安装的版本

   ```shell
   nvm -v
   npm -v
   node -v
   hexo -v
   ```



# 二、初始化博客

1. 切换目录到blog 

   ```shell
   cd blog
   ```

2. 初始化hexo博客

   ```shell
   hexo init
   ```

3. 结果如下图所示在blog文件夹下生成博客的初始化文件
    
    ![图3](/images/papers/Hexo+Netlify2createblog/init7.png)

    ![图4](/images/papers/Hexo+Netlify2createblog/initfile8.png)



4. 在终端中执行以下命令生成博客

   ```shell
   hexo g
   hexo s
   ```

   

5. 在浏览器中打开以下地址，浏览自己的博客

   ```http
   http://localhost:4000/
   ```

   

6. 效果如下图所示
    ![图5](/images/papers/Hexo+Netlify2createblog/9.png)


   

   

# 三、将博客部署至Github

1. 访问Github官网并登录自己的账号（没有账号先注册再登陆）

2. 创建一个新仓库步骤如下

   1. - 点击右上角加号，并选择New repository![图6](/images/papers/Hexo+Netlify2createblog/10.png)

      - 在弹出的新建页面中需要注意Repository name的填写，具体细节点击[参考1](https://www.bilibili.com/video/BV1Yb411a7ty/  "手把手教你从0开始搭建自己的个人博客" )

        

        

   

3. 回到终端安装deploy包并进行相关配置

   

   ```shell
   npm install hexo-deployer-git –save #安装部署文件
   vim _config.yml  #用vim修改博客配置文件config.yml
   ```

   - _config.yml按“i键 ”进入插入inset模式

   - 在_config.yml的末尾修改内容如下：

     ```shell
     deploy:
       type: git
       repository: https://{你的token}@github.com/{git用户名}/{git用户名}.github.io.git  #你的仓库地址
       branch: master
     
     ```

     笔者这个改后的内容如下
     ![图7](/images/papers/Hexo+Netlify2createblog/12.png)


     

   - 修改完成后 按shift+: 键 进入cmd 模式 ，并输入 wq 回车

   - ==token的获取==：

     1. 打开自己的github点击设置--->点击Developer settings--->在Personal access tokens 下面的列表中选择Tokens(classic),进行设置，在设置菜单中的复选框中全部点上对勾给足权限。![图8](/images/papers/Hexo+Netlify2createblog/20.png)
     2. 点击最下面的Generate token 生成token ![图9](/images/papers/Hexo+Netlify2createblog/21.png)  

   

4. 设置git 邮箱和用户名

   ```shell
   git config --global user.name Your Name
   git config --global user.email you@example.com
   ```

5. 部署博客

   ```shell
   hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
   hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
   hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
   ```

   部署完成后你就可以在浏览器中打开   “你的github用户名.github.io”  来访问自己的博客了



# 四、更换主题

等待后续更新
