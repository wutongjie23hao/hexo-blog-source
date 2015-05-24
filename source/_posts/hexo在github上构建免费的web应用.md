title: hexo在github上构建免费的web应用
date: 2015-05-24 14:40:47
tags: 
- hexo
categories: 
- 技术
---
# Hexo在github上构建免费的web应用 #
本文简单记录在github上构建web应用，包括Hexo安装、Hexo的一些基本命令、Hexo的一些问题、为web网站添加评论和微博秀。<!--more-->
## hexo安装 ##
参考：[Hexo在github上构建免费的Web应用](http://blog.fens.me/hexo-blog-github/)
1. 下载[nodejs](https://nodejs.org/download/)，安装以后，会自动将node的一些命令添加到环境变量，包括npm这个安装工具。
2. 在命令行中输入"npm install -g hexo"，就安装完毕，然后运行"hexo version"，有显示就行。

## hexo基本命令 ##
可以从[我的github](https://github.com/wutongjie23hao/hexo-blog-source)上fork我的文件（忽略第一个步骤），或者自己构建。
1. 新建文件夹，然后在命令行中进入相应目录（假如名字为hexo-blog-source)，执行命令``npm init``或者之前没有新建文件夹，然后执行命令``hexo init hexo-blog-source``，hexo会自动创建一个文件夹，名字为"hexo-blog-source"。
2. 修改根目录下的"_config.yml"文件，修改参考我的源代码。
2. 进入"hexo-blog-source",运行命令``npm install``,原因是在git的时候，忽略了"node_modules"这一个文件夹，如果不运行这个命令，会出现"hexo 没有在本地"什么的错误提示。运行这个命令以后，就能在根目录下生成一个叫"node_modules"的文件夹，这样就能接着往下跑了。
3. 运行命令``hexo g[erate] -p 端口号（默认4000）``,会在_config.yml中public_dir对应的目录产生静态文件。(运行命令``hexo g -d``可以直接完成部署，只是我的总是报错，暂未解决，部署的话后面会有介绍)
4. 运行命令``hexo s[erver]``，会启动hexo自带的服务器，然后你就能在<http://localhost:4000>看到自己的网站雏形了。
5. 运行命令``hexo new "xxx" ``，会在source/_posts/文件夹下生成一个md文件，编辑即可。

## hexo部署 ##
这个不想多讲，因为我的运行有错误，
```bash
Error: spawn git ENOENT
    at exports._errnoException (util.js:746:11)
    at Process.ChildProcess._handle.onexit (child_process.js:1053:32)
    at child_process.js:1144:20
    at process._tickCallback (node.js:355:11)
```
我参考了[leyar的日志](http://www.leyar.me/Digitalocean-vps-nginx-setup/)，虽然我的是用的github报错了，但还是没有解决。然后我就手工上载到我的github空间。推荐几个网站:[hexo官方部署文档](http://hexo.io/zh-cn/docs/deployment.html),还可以参考[leyar的hexo部署日志](http://www.leyar.me/create-a-blog-with-hexo-in-ubuntu/),尽管他的是在Linux下的，windows下也一样。

## hexo问题 ##
主要是中文乱码问题：我使用汉语修改了皮肤和配置文件里面的一些东西以后，出现乱码。主要是文件编码是ANSI，然后转换成utf8就行。

## 设置hexo皮肤 ##
我使用的是[A-limon的pacman皮肤](https://github.com/A-limon/pacman)。他使用的markdown样式表为[chjj的marked](https://github.com/chjj/marked),对于GFM好像支持，但是有些支持的不是很好，待修正。你也可以选则[别的皮肤](https://github.com/tommy351/hexo/wiki/Themes)。
1. 将中意的theme下载到/themes/文件夹下，比如我的是pacman，那么就对应/themes/pacman。
2. 编辑项目根目录文件下的_config.yml,找到theme一行，改成``theme:pacman``即可。
3. 此时再跑，奇迹发生了吧。

## 添加about、评论、分享、微博秀等插件 ##
首先，我使用的pacman文件目录下有个_config.yml，设置对应项的值就可以改变。
```bash
#### Comment
duoshuo: 
  enable: true  ## duoshuo.com
  short_name: wutongjie23hao   ## duoshuo short name.

#### Share button
jiathis:
  enable: true ## if you use jiathis as your share tool,the built-in share tool won't be display.
  id: 2033935 ## e.g. 1501277 your jiathis ID. 
  tsina: 1745728450 ## e.g. 1664838973 Your weibo id,It will be used in share button.
```
其中评论用的是多说，分享用的是jiathis,已经做了本土化处理。
当然，如果是别的皮肤的话，要自己设置，设置多说评论、百度分享、微博秀参考[zippera's blog](http://zipperary.com/2013/05/30/hexo-guide-4/),然后，设置disqus评论，参考[粉丝日志](http://blog.fens.me/hexo-blog-github/),不过很慢。皮肤默认的分享也是twitter、google+等登不上的东东。
** 备注 **：多说中，
```js
data-thread-key="<%- page.path %>"
data-title="<%- page.title %>"
data-url="<%- page.permalink %>"
```

## 显示数学公式 ##
参考[粉丝日志](http://blog.fens.me/hexo-blog-github/)。
* themes/**/layout/_partial/ 文件夹下添加mathjax.ejs.代码为：

```js
<!-- mathjax config similar to math.stackexchange -->

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
      }
    });
</script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Queue(function() {
        var all = MathJax.Hub.getAllJax(), i;
        for(i=0; i < all.length; i += 1) {
            all[i].SourceElement().parentNode.className += ' has-jax';
        }
    });
</script>

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```
* 在themes/pacman/layout/_partial/after_footer.ejs里添加对mathjax.ejs的引用。看源码。

## 其它 ##
* [从零开始nodejs系列文章](http://blog.fens.me/series-nodejs/)
* [添加RSS、sitemap、百度统计或google analytics、fork me on github](http://zipperary.com/2013/06/02/hexo-guide-5/)(pacman上有选项，我还没做)
* [hexo博客的配置和使用](http://zipperary.com/2013/05/29/hexo-guide-3/)
* [托管博客到STDYUN](http://zipperary.com/2013/11/13/blog-to-stdyun/)
* 工具:[制作ico](http://www.faviconer.com/)、[Image to data URI](http://websemantics.co.uk/online_tools/image_to_data_uri_convertor/)
* [整合google自定义搜索CSE](http://www.neoease.com/integrate-google-custom-search-into-wordpress/),我登不上谷歌，所以没有试一下
