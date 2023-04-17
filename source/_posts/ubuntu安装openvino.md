---
title: ubuntu安装openvino
tags:
  - ubuntu
  - openvino
categories: 经验分享
abbrlink: d09c2aa
date: 2023-02-13 11:57:44
---

### 一、安装环境:

1. 已有的环境

   ```text
   ubuntu18.04LTS
   ```

2. 准备安装的环境

<img src="/images/posts/openvino/1.png" style="zoom:80%;" />



### 二、检查自己的python环境：

18.04的ubuntu自带的python版本为3.59，而openvino对python版本有要求，因此我们需要将ubuntu的python进行更新具体操作如下：

```shell
sudo add-apt-repository ppa:jonathonf/python-3.8
sudo apt-get update
sudo apt-get install python3.8 
sudo apt-get install python3-pip
sudo pip3 install --upgrade pip
```

执行以上命令可能会遇到的错误如下：

update-alternatives: error: no alternatives for python  [点击此处查看解决方法](https://zhuanlan.zhihu.com/p/159483149)



### 三、安装openvino

1. 更新pip镜像源[方法参考](https://blog.csdn.net/weixin_42214237/article/details/117594416?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-5-117594416-blog-107920107.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-5-117594416-blog-107920107.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=9)

2. ```shell
   apt install python3.8-venv
   python3 -m venv openvino_env
   source openvino_env/bin/activate
   python -m pip install --upgrade pip
   ```

3. ```shell
   pip install openvino-dev[caffe,pytorch,tensorflow2,ONNX]==2022.3.0 
   ```

   中括号中可以选择的模型[参考]([下载英特尔® 发行版 OpenVINO™ 工具套件 (intel.cn)](https://www.intel.cn/content/www/cn/zh/developer/tools/openvino-toolkit/download.html))中的框架部分

4. ```shell
   mo -h #测试是否安装成功
   ```

### 四、安装openvino_notebooks



具体安装过程，可以参考[链接]([Ubuntu · openvinotoolkit/openvino_notebooks Wiki (github.com)](https://github.com/openvinotoolkit/openvino_notebooks/wiki/Ubuntu)),笔者在此不再赘述，此部分安装过程比较慢，耐心等待即可。

### 五、官方demo测试

这里给出笔者在官网找到的测试demo点击[链接]([您好图像分类 — OpenVINO™ 文档 — 版本（最新）](https://docs.openvino.ai/latest/notebooks/001-hello-world-with-output.html#))即可进行相关验证学习。
