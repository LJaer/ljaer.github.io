---
title: 使用Hexo搭建博客（一），搭建博客的过程
date: 2016-09-24 11:30:13
categories: 技术文档
tags: Hexo
---

### 1.安装[Git](https://git-scm.com/ "Git")
　　根据系统（Win，Mac，Linux）选择相应的git进行安装

　　[注册](https://github.com/ "注册")Github账号
　　因为是托管到Github上，所以需要注册一个账号。
　　注意一定要验证Github的验证邮件

　　配置SSH公钥
　　远程代码是基于SSH的，所以需要SSH的相关配置。方法是先在本地生成SSH公钥，然后添加到Github上面。具体的操作如下：
　　设置你的邮箱和用户名：
```shell
git config --global user.email "673820543@qq.com"
git config --global user.name "LJaer"
```

　　生成密钥，设置密码，输入的密码不显示（也可以不设置，按三次回车，密码为空）
```shell
ssh-keygen -t rsa -C "673820543@qq.com"
```

　　上述的命令成功后，会得到id_rsa和id_rsa.pub两个文件，可能在C:\Users\Administrator\.ssh文件夹里，没有的话，就用Everything搜一下。
　　把SSH密钥添加到Github上
　　登陆Github后，点击settings，然后进入SSH keys，把id_rsa.pub文件里内容添加进去就好了。

### 2.安装[Node.js](https://nodejs.org/en/ "Node.js")
　　选择LTS版本进行安装
### 3.安装Hexo
　　Hexo的安装需要借助Node.js的npm命令，可以理解为Hexo是Node.js的模块。操作的方式是在任意的位置单击鼠标右键，选择Git bash命令，在里面输入：
```shell
npm install -g hexo
```

　　卸载的话，自然是把上面命令中的install替换成uninstall即可执行卸载。
### 4.创建Hexo文件夹并初始化Hexo
　　Hexo文件夹就是你后面博客的文件夹。第一步先在某个盘符下新建一个文件夹，重命名（英文字母），假设你是在D盘下建立了一个名叫Hexo的文件夹，那么路径就是D:\hexo （后续的操作大多在这个文件夹里进行）；第二步进入Hexo文件夹单击右键，依旧选择Git bash这一命令，输入以下命令，博客所需要的文件都已经自动建立好了，这比jekyll操作简单多了。
```shell
hexo init
```

### 5.安装依赖包
```
npm install
```

### 6.预览本地博客
　　一系列的安装命令之后，本地博客就算搭建好了，输入如下的命令
```shell
hexo g
hexo s
```

　　然后在浏览器地址栏中输入localhost:4000或者127.0.0.1:4000就可以查看本地的博客了。

　　不出意外的话，它应该是像下图这个样子的（图片来源于网络）。注意这里仅仅是本地博客，其他地方看不到。第一步操作到这里就结束了。

![201909002](http://oe53dpmqz.bkt.clouddn.com/20160929002.png)

### 7.建立和用户名对应的仓库
　　建立和用户名相对应的仓库，比如：我的用户名是LJaer,那么我的仓库就必须是ljaer.github.io。

### 8.部署远程博客
　　编辑Hexo目录下的配置文件_config.yml,在最下面输入以下内容，注意把里面的LJaer替换成你的用户名
```
deploy:
  type: git
  repo: git@github.com:LJaer/ljaer.github.io.git
  branch: master
```

　　部署远程博客，输入以下命令
```
hexo g
hexo d
```

　　出现下面的提示表示部署成功
```
INFO Deploy done: git
```

　　部署好了后，在浏览器地址栏中输入你的仓库名来访问，我的是ljaer.github.io。注意一点，第一次部署的话，可能需要等待一会（一般不到10分钟就好了）才能生效，以后每次部署就可以直接访问。到这里基本的博客就搭建好了。

### 9.Hexo的基本命令
　　Hexo基本常用的命令就四个，而且还可以使用组合命令。基本命令如下：
```
hexo g = hexo generate  #生成
hexo s = hexo server  #启动本地预览
hexo d = hexo deploy  #远程部署
hexo n "文章标题" = hexo new "文章标题"  #新建一篇博文
```

　　组合命令：
```
hexo s -g  #等同先输入hexo g，再输入hexo s
hexo d -g  #等同先输入hexo g，再输入hexo d
```

### 10、注意
　　出现其他任何的问题，先删除博客目录下的db.json文件，然后清理再部署远程博客，操作时输入以下的命令
```
hexo clean
hexo d -g
```

### 参考链接

在搭建过程中，参考以下文章进行搭建

起今执行：http://www.jianshu.com/notebooks/1045230/latest



