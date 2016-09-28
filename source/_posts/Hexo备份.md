---
title: Hexo备份
date: 2016-09-26 16:20:44
categories: 技术文档
tags: Hexo
---

### 一、需求：
在Windows和Mac下需要对Hexo进行管理和更新。

### 二、思路
创建分支，一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页。

### 三、搭建的流程

1、创建仓卡，ljaer.github.io;
2、在本地创建ljaer.github.io;
3、在本地ljaer.github.io文件夹下一次执行npm install hexo、hexo init、npm install 和 npm install hexo-deployer-git;
4、在本地ljaer.github.io文件夹下
```
#git初始化
git init
#创建hexo分支
git checkout -b hexo
#git 文件添加
git add .
#git 提交
git commit -m "init"
#添加远程仓库
git remote add origin git@github.com:LJaer/ljaer.github.io.git
#push到hexo分支
git push origin hexo
```

5、修改_config.yml中的deploy参数，分支应为master;
6、依次执行git add .、git commit -m "..."、git push origin hexo提交网站相关的文件;
7、执行hexo g -d生成网站并部署到GitHub上

这样一来，在GitHub上的git@github.com:LJaer/ljaer.github.io.git仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。

### 四、日常的改动流程
在本地对博客进行修改（添加新博文、修改样式等等）后，通过下面的流程进行管理。

1. 依次执行git add .、git commit -m "..."、git push origin hexo指令将改动推送到GitHub（此时当前分支应为hexo）；
2. 然后才执行hexo g -d发布网站到master分支上。

### 五、本地资料丢失后的流程
当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：

1. 使用git clone git@github.com:LJaer/ljaer.github.io.git拷贝仓库（默认分支为hexo）；




