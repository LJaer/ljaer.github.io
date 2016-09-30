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
注册之后得到了id，把id添加到jiathis.ejs文件中；没改动的话是在第22行的uid那里。
再在主题配置文件中jiathis的enable改为true启用，也同样填上id。
1
2
3
jiathis:
  enable: true ## if you use jiathis as your share tool,the built-in share tool won't be display.
  id:    ## e.g. 1889330 your jiathis ID.


### 1.添加『微搜索』
　　现在的文章还不多，使用目录和标签就可以快速找到文章，这是一种方式。对于习惯用搜索的用户来说，特别是后续文章积累到一定的程度之后，想要快速找到自己想看到的文章就比较困难，我自己就希望实现站内搜索的功能。而静态网页和动态的诸如Wordpress不同，内置的谷歌搜索，但是显然在国内直接不能实现站内搜索的，你需要采取其他的措施。查询了一下，使用百度和swiftype都可以为Hexo实现站内搜索。
　　swiftype老是提示Please use your work email，注册不成功。这里我使用[百度站内搜索](http://zn.baidu.com/cse/wiki/index?category_id=17 "百度站内搜索")。

1.注册之后得到key，然后把key填到到D:\Hexo\themes\jacman\layout\_partial\tinysou_search.ejs文件；
1
engineKey: ''  #e.g.  'eb4726b2a0ea6b569b79'
2.把主题配置文件_config.yml修改启用，填上你的id就可以。
1
2
3
tinysou_search:     ## http://tinysou.com/
  enable: true
  id:  ## e.g. eb4726b2a0ea6b569b79  for your tiny search id


2.添加『多说评论』
　　评论系统国内使用比较多的是多说，先注册一下，然后在主题配置文件中填上你的用户名；
在多说进行注册，获得通用代码，将通用代码粘贴到D:\Hexo\themes\jacman\layout\_partial\post\comment.ejs文件里面；
1
2
3
4
5
<% if (theme.duoshuo.enable && page.comments){ %>
<section class="comment">
    #此处粘贴你的通用代码
</section>
<% } %>
在主题配置文件中，填上你多说的用户名
1
duoshuo_shortname:    ## e.g. qjzhixing  your duoshuo short name.


二、Hexo的几款插件
　　Hexo里面默认有一些插件，这里推荐几款可能对个人有用的插件。输入对应的命令安装一下，然后设置一下就可以。
1.导入『Wordpress数据』
　　开篇我说过我写博客的基本经历，是从Wordpress转移过来的，写了一段时间之后，文章全部在那里面，如果一篇篇的复制粘贴那工作量就太大了。好在Hexo提供了Wordpress插件，可以一次性把wordpress数据导入到Hexo博客，html文件都转换成了Markdown文件，非常的方便，有图片的更改一下图片的路径就好了。
首先导出wordpress数据，得到的回事一个xml格式的文件，先把这个复制到Hexo文件夹下，假设文件是wordpress.xml。
安装好wordpress插件，再使用迁移命令就可以实现从Wordpress到Hexo的转移。
1
2
npm install hexo-migrator-wordpress --save
hexo migrate wordpress wordpress.xml
2.添加『RSS订阅』和『百度sitemap』
　　RSS订阅和百度sitemap（站点地图，方便搜索引擎的收录）的安装和设置做法相似，所以放在一起说明。输入的命令分别是：
1
2
npm install hexo-generator-feed --save
npm install hexo-generator-baidu-sitemap --save
　　然后在博客配置文件_config.yml中添加启动
1
2
3
plugins:
- hexo-generator-feed
- hexo-generator-baidu-sitemap
　　对于百度地图，还需要添加
1
2
3
#sitemap
baidusitemap:
    path: baidusitemap.xm
　　添加好了之后，测试一下RSS和百度地图是否生效，百度地图是访问qjzhixing.com/sitemap.xml可以查看，如果能正常访问说明可用。
3.添加『CNZZ统计/百度统计』
　　CNZZ统计和百度统计都不算是Hexo的插件，但我个人觉得还是充当了插件的作用，所以就放在了这里。做法是先注册账号，然后添加网址就设置好了。CNZZ和百度统计的设置和做法相似，两种统计我都有测试过，没有问题。是先试过百度的，然后转换到了CNZZ上，所以就那CNZZ作为例子说明一下。
1.在CNZZ网站注册一个账号，添加网站后，得到各个形式的代码，任选其一；
2.在D:\Hexo\themes\jacman\layout\_partial文件夹下新建一个cnzz_tongji.ejs文件，把你的代码粘贴在第一行和最后一行之间（中间是我的，替换成你自己的）；
1
2
3
4
5
6
<% if (theme.cnzz){ %>
<script type="text/javascript">
    var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");
    document.write(unescape("%3Cspan id='cnzz_stat_icon_1256211004'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s95.cnzz.com/z_stat.php%3Fid%3D1256211004%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));
</script>
<% } %>
3.在footer.ejs文件中适当的位置添加你的代码，这是我的代码；
1
2
3
4
<script type="text/javascript">
    var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");
    document.write(unescape("%3Cspan id='cnzz_stat_icon_1256211004'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s95.cnzz.com/z_stat.php%3Fid%3D1256211004%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));
</script>
4.在主题配置文件中加入下面代码启用CNZZ统计，注意不要添加站点id，填了的话就不显示图标了。
1
2
## Analytics
cnzz_tongji: true
三、购买和绑定顶级域名（可选）
　　域名的购买多数人都推荐在Godaddy购买，我的qjzhixing.com这个域名也是。名气较大，支持支付宝付款。解析和管理域名在Dnspod上面进行，两个都需要注册，这个简单不用说，说下实现域名绑定的过程。
1.把购买好的域名添加到Dnspod里面，得到两个默认的NS地址，此时顺便添加以下A记录，主机记录有两个：@和www，记录类型默认A，而且记录值都一样，填写192.30.252.153；

2.使用Dnspod解析域名的话，就要将GoDaddy的NS设置为Dnspod提供的地址。做法是在GoDaddy的Nameservers里面添加Dnspod的NS，也就是图中中间的那两个记录值。

3.在博客的D:\Hexo\source目录下，新建名为CNAME的文本文件，没有后缀，在里面添加你的域名。比如我的就是qjzhixing.com，如果你想用www.qjzhixing.com域名就在里面填相应的域名。添加之后尽量就不要改了。
1
qjzhixing.com
　　注意，绑定好了有可能还需要等待一段时间才能生效。我绑定域名的过程进展不是那么的顺利，原因是收不到GoDaddy的验证邮件。没有验证邮件是无法添加Dnspod的NS地址的，也就不能实现绑定。试过QQ邮箱、163邮箱，最后换到了Gmail邮箱都不行，奇怪的是，自己注册和买域名的时候能受到邮件，但是就是验证邮件收不到，垃圾箱里面也没有。没有办法，只得在网上找GoDaddy的客服，等待了11分钟之后客服回话了，给重新发了一封验证邮件，问题终于解决了。所以，如果遇到什么问题，还是要找对Keyman。