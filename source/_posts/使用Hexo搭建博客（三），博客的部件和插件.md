---
title: 使用Hexo搭建博客（三），博客的部件和插件
date: 2016-09-29 11:17:20
categories: 技术文档
tags: Hexo
---

## 一、博客的零部件
### 1.添加『友情链接』
　　友情链接的文件在pacman/layout/_widget/links.ejs文件里面添加，同样需要在主题配置文件中设置显示。在<ul>和</ul>标签之间添加，格式参考
```
<div class="linkslist">
  <p class="asidetitle"><%= __('links') %></p>
    <ul>
      <li><a href="http://blog.csdn.net/zk673820543" target="_blank" title="CSDN">zk的CSDN博客</a></li>
      <li><a href="https://github.com/LJaer" target="_blank" title="GitHub">LJaer的github</a></li>
    </ul>
</div>
```

　　在pacman/_config.yml文件中，添加links
```
widgets: 
- links
```

### 2.添加[『新浪微博秀』](http://app.weibo.com/tool/weiboshow "『新浪微博秀』")
　　微博秀这个可以根据个人的意愿。先在[微博秀](http://app.weibo.com/tool/weiboshow "微博秀")开通一下。获取到如下代码：把得到的代码直接保存到pacman/layout/_widget/weibo.ejs文件里，没有就新建一个；在主题配置文件pacman/_config.yml的部件里加上微博秀。
```
widgets:
- weibo
```

### 3.添加[『JiaThis分享』](http://www.jiathis.com/ "『JiaThis分享』")
　　博客在前期需要大量推广，即使你写的文章再好，别人也不一定能看到，或者别人看到了也不会认真阅读，这是正常的。不妨主动自己主动一点，把自己的文章推广一下，也能帮助自己博客提高访问量。微博、微信和QQ空间都是很好的传播平台，需要利用好。所以就需要一键分享的功能。不少人用的百度的，但个人对JiaThis更感兴趣一点。样式多，支持平台多，重要的是方便。
注册之后得到了id，把id添加到pacman/layout/_partial/post/jiathis.ejs文件中；没改动的话是在第22行的uid那里。
再在主题配置文件中jiathis的enable改为true启用，也同样填上id。
```
#### Share button
jiathis:
  enable: true ## if you use jiathis as your share tool,the built-in share tool won't be display.
  id: 2111669   ## e.g. 1501277 your jiathis ID. 
  tsina: 2554366815 ## e.g. 1664838973 Your weibo id,It will be used in share button.
```

### 4.添加[『多说评论』](http://duoshuo.com/ "『多说评论』")
　　静态博客要使用第三方评论系统，pacman配置了多说评论系统（/themes/pacman/_config.yml），默认关闭，只要将其打开即可:false->true。直接用你的微博/豆瓣/人人/百度/开心网帐号登录多说，即可发表平评论。
```
#### Comment
duoshuo: 
  enable: true  ## duoshuo.com
  short_name: ljaer   ## duoshuo short name.即为注册时，域名xxx.duoshuo.com的xxx
```



### 1.添加『微搜索』
　　现在的文章还不多，使用目录和标签就可以快速找到文章，这是一种方式。对于习惯用搜索的用户来说，特别是后续文章积累到一定的程度之后，想要快速找到自己想看到的文章就比较困难，我自己就希望实现站内搜索的功能。而静态网页和动态的诸如Wordpress不同，内置的谷歌搜索，但是显然在国内直接不能实现站内搜索的，你需要采取其他的措施。查询了一下，使用百度和swiftype都可以为Hexo实现站内搜索。
　　swiftype老是提示Please use your work email，注册不成功。这里我使用[百度站内搜索](http://zn.baidu.com/cse/wiki/index?category_id=17 "百度站内搜索")。

1.注册之后得到key，然后把key填到到D:\Hexo\themes\jacman\layout\_partial\tinysou_search.ejs文件；
engineKey: ''  #e.g.  'eb4726b2a0ea6b569b79'
2.把主题配置文件_config.yml修改启用，填上你的id就可以。

tinysou_search:     ## http://tinysou.com/
  enable: true
  id:  ## e.g. eb4726b2a0ea6b569b79  for your tiny search id





## 二、Hexo的几款插件
　　Hexo里面默认有一些插件，这里推荐几款可能对个人有用的插件。输入对应的命令安装一下，然后设置一下就可以。

###１.添加『RSS订阅』和『百度sitemap』
　　RSS订阅和百度sitemap（站点地图，方便搜索引擎的收录）的安装和设置做法相似，所以放在一起说明。输入的命令分别是：
```
npm install hexo-generator-feed --save
npm install hexo-generator-baidu-sitemap --save
```

　　然后在博客配置文件修改Hexo\_config.yml中添加启动
```
Plugins:
- hexo-generator-feed
- hexo-generator-baidu-sitemap
```

　　对于百度地图，还需要添加
```
#sitemap
baidusitemap:
    path: baidusitemap.xml
```

　　添加好了之后，测试一下RSS和百度地图是否生效，百度地图是访问http://localhost:4000/baidusitemap.xml可以查看，如果能正常访问说明可用。

### 2.添加『CNZZ统计』
　　CNZZ统计不算是Hexo的插件，但我个人觉得还是充当了插件的作用，所以就放在了这里。做法是先注册账号，然后添加网址就设置好了。
- 1.在CNZZ网站注册一个账号，添加网站后，得到各个形式的代码，任选其一；
- 2.在Hexo\themes\pacman\layout\_partial文件夹下新建一个cnzz_tongji.ejs文件，把你的代码粘贴在第一行和最后一行之间（中间是我的，替换成你自己的）；
 
```html
<% if (theme.cnzz){ %>
<script type="text/javascript">var cnzz_protocol = (("https:" == 
document.location.protocol) ? " https://" : " http://");
document.write(unescape("%3Cspan id='cnzz_stat_icon_1260464597'%3E%3C/span%3E%3Cscript src='" 
+ cnzz_protocol + 
"s95.cnzz.com/z_stat.php%3Fid%3D1260464597%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));
</script>
<% } %>
```

- 3.在footer.ejs文件中适当的位置添加你的代码，这是我的代码；
```html
<script type="text/javascript">var cnzz_protocol = (("https:" == 
document.location.protocol) ? " https://" : " http://");
document.write(unescape("%3Cspan id='cnzz_stat_icon_1260464597'%3E%3C/span%3E%3Cscript src='" 
+ cnzz_protocol + 
"s95.cnzz.com/z_stat.php%3Fid%3D1260464597%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));
</script>
```

- 4.在主题配置文件中加入下面代码启用CNZZ统计，注意不要添加站点id，填了的话就不显示图标了。
```
#### Analytics
cnzz_tongji: true
```
