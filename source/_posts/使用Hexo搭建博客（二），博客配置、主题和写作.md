---
title: 使用Hexo搭建博客（二），博客配置、主题和写作
date: 2016-09-29 10:33:13
categories: 技术文档
tags: Hexo
---

### 1.博客的整体配置
　　博客的整体配置在Hexo\_config.yml文件中进行。默认使用的主题是landscape，主题的配置在Hexo\themes\landscape\_config.yml。主题的配置可以暂时不动，等到更换了自己满意的主题后再进行。先来说一下博客的整体配置，也就是打开Hexo\_config.yml文件，更改里面的部分内容。简化起见，其他内容先不做更改，只更改# site下面的内容。
```
# Site
title: 冗码生涯  #填写网站名，会在标签页上显示
subtitle: 只有做不好事的人，没有做不好的事  #副标题，网站名下面
description: 个人博客   #网站描述，便于搜索引擎用关键词检索
author: LJaer   #作者
language: zh-CN     #语言，中文
timezone: Asia/Shanghai     #时区
```

　　更改完毕之后，启动本地预览，在浏览器中访问localhost:4000预览以下配置的效果，如果满意的话，Ctrl+C关闭预览，同步到Github上面即可。
```
hexo s -g
hexo d -g
```

### 2.更换主题
　　使用Hexo更换主题还算方便，先使用克隆命令安装好主题，然后更改一下博客的配置文件Hexo\_config.yml里面的主题名称就好了。关于主题的选择，每个人的喜好不同，你可以到[Hexo官方主题](https://hexo.io/themes/ "Hexo官方主题")页面选择自己喜欢的主题，里面收录的主题相对来说功能更齐全，还有[wiki](https://github.com/hexojs/hexo/wiki/Themes "wiki")里面的主题也还可以 。我选用的是Pacman主题。后面都是针对于Pacman主题的介绍。说明一点：使用他人的主题，一定要保留主题作者的信息（在博客最下面显示），表示对作者的尊重。

　　安装主题
　　在博客目录Ｈexo下右键点击Git Bash，输入以下命令。其他的主题也类似操作。
```
git clone git@github.com:A-limon/pacman.git
```

　　启用主题
　　修改博客目录Ｈexo\_config.yml中的theme属性，将其设置为pacman。

```
theme: pacman
```

　　更新主题
　　在主题更新之前，一定要备份好主题目录下的_config.yml文件，尤其是到后面修改了很多配置之后。

　　到这里主题的更换就好了，启动本地预览一下，可以的话就同步到Github上面吧。
### 3.主题的配置
　　主题的配置当然就是在Hexo\themes\pacman\_config.yml文件里面了。一般而言，主题的作者都会有对主题的相关介绍，看他介绍的修改就可以了。我主要针对导航栏和右边栏小部件举例简单说明一下，后面你就知道如何配置了。
```
menu:  #导航栏
  主页: /
  归档: /archives
  关于: /about  #介绍一下你自己
#### Widgets 
widgets: ## 右边的零部件,可以根据自己喜好增减
- category  #目录
- links  #友情链接
- tagcloud  #标签云（也可以选用标签，上面显示数值）
- rss   #RSS
- weibo #微博秀，需要在微博上开通
```

　　导航栏上如何添加新页面呢？比如关于页面，就是输入下面命令，新建一个页面，在里添加内容即可。
```
hexo new page "about"
```

　　导航栏里的文件都在Hexo\source\目录下，而零部件widgets的文件都在Hexo\themes\pacman\layout\_widget\文件夹里，在相应的文件里修改，然后预览再部署。注意，修改任何的配置内容，都需要生成之后才有效。

### 4.写作
　　博客基本配置完成了，主题也更换了，开始写一篇文章吧！上一篇Hexo基本命令中有如何新建文章的命令，使用hexo n那个命令新建文章就好了，你也可以在博客目录Hexo\source\_posts中新建一个后缀为.md的文件，使用文本编辑器在里面采用Markdown来书写，效果一样。

　　添加文章抬头信息
　　Hexo默认新建的文章抬头已有title、date、tags等属性，可能缺乏categories和meta标签，想要指定目录就需要添加categories属性，而meta标签则是为了便于搜索引擎的收录。想要修改的话，可以打开Hexo\scaffolds\post.md文件在里面添加。
```
title:  #文章标题
date:  #时间，一般不用改
categories:  #目录分类
tags:  #标签，格式可以是[Hexo,总结]，中间用英文逗号分开
keywords:  #文章关键词，多个关键词用英文逗号隔开
```

　　文章图片的存放
　　想要在文章中插入图片的话，可以按照Markdown语法来插入，格式为\!\[图片名称\]\(图片地址\)。图片的存放有两种方式：在本地Hexo\source\目录下新建一个存放图片的文件夹，比如images，然后把想要插入的图片放在里面，插入图片的路径；第二种方法是把图片上传到网络，然后插入图片路径。推荐使用第二种。
　　推荐两个比较好用的：
- 图床；无需注册，方便快捷。
- 七牛云存储；需要注册，免费，空间大，速度快。
　　
到了这一步，基本的配置已经完成了，博客写作需要注意的地方也提到了。但是可能还没有完，还有一些细节的完善，或者你自己想要定制能凸显你个性的部件。