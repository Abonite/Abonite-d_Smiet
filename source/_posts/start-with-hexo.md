---
title: 使用Hexo搭建自己的个人Blog
date: 2021-12-18 22:56:40
comment: 'gitalk'
categories:
- 技术
tags: 
- 技术
- hexo
---

## 事故

自从前任服务器爆炸之后就不知道要把各种乱七八糟的想法放在哪里了。前任服务器的配置很糟糕，单核，512Mb内存，我在上面运行了一个wordpress，一个mysql外加php。那台服务器并没燃烧起来，不过访问就成了火葬场。这样看来，其实还是烧起来了，只不过不是服务器，而是维护者和访问者。

前一阵子，我发现所有需要经过前服务器的访问都挂掉了。尝试重启服务器，重装服务器，都没有出现奇迹。现在前服务器已经处于不可访问的状态。于是我只能再找一台服务器，重新搭建Blog，换掉wordpress，试用一些其他的框架。

## 如何开始？

Wordpress对我来说确实有些大材小用了。如果只是利用网站写些文字，展示一些图片，那么简单但不平凡的Hexo也许更适合我。作为一个静态框架，hexo可以为我提供我需要的一切功能。

### 安装依赖

首先需要检查计算机上是否安装了node.js和git。我们需要使用node.js和git安装hexo框架，并且使用git备份我们的网站。

{% codeblock lang:shell %}
node -v
npm -v
git --version
{% endcodeblock %}

一般来说，以上软件无脑选择版本最新的稳定版即可。如果版本过低，可能会引起一些问题。比如版本过低时，运行hexo g时可能会报出“line.matchAll is not function”错误，此时应该升级nodejs到12.0.0以上。具体node.js版本与hexo版本的对应关系，可以查阅hexo官方的文档 [概述部分](https://hexo.io/zh-cn/docs/)。

### 初始化Hexo

确认一切无误后，就可以运行

```shell
npm install -g hexo-cli
```

安装hexo。

待安装完成后，选定希望构建hexo的路径，并执行

```
hexo init <path of hexo (folder)>
cd <path of hexo (folder)>
npm install
```

新建完成后，目录下应该会多出一些文件夹和文件。此时如果运行hexo g，hexo s，即可在localhost:4000看到hexo页面了。

### 安装主题

如果你觉得原版的Hexo主题已经足够好，那么就不需要进行这一步。如果你同我一样希望更改hexo的主题，那么你需要访问[这个链接](https://hexo.io/themes/)，或者从网上寻找你想用的hexo主题。

我选择了Fluit，这个主题的Github页面在[这里](https://github.com/fluid-dev/hexo-theme-fluid)。进入hexo根目录下的theme文件夹，并且使用git命令拉取文件

```shell
git clone https://github.com/fluid-dev/hexo-theme-fluid.git fluid
```

然后，进入hexo根目录下，使用vim编辑_config.yml，修改标题，简介，语言，时区等所有需要的信息。具体参数可以参考[官方文档](https://hexo.io/zh-cn/docs/configuration)。当然，主题也需要进行设置，可以直接编辑./theme/fliud/_config.yml，具体参数可以参考fluid的[官方文档](https://fluid-dev.github.io/hexo-fluid-docs/guide/#%E5%85%B3%E4%BA%8E%E6%8C%87%E5%8D%97)。

### 配置git

给自己的网站开一个仓库，更新之后把代码push上去。记得先配置git密钥。

### nginx代理

使用nginx时，不需要运行hexo s启动服务，直接设置根路径为hexo根路径下的public文件夹下即可。更新文件后，使用hexo g生成页面。

### vscode远程编辑

使用SSH Remote远程连接服务器，运行

```shell
hexo new post title_of_new_post
```

然后进入hexo根路径的source文件夹下，就可以看到新生成的markdown文件。

---
{% blockquote %}
We always have some impractical illusions, about our life, about the people around us, about the stars in the sky.
我们总有些不切实际的幻想，关于我们的生活，关于我们身边的人，关于天上的星星。
{% endblockquote %}