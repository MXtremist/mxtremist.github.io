---
layout:  post
title:  从零开始的搭建个人博客生活
date:  2020-06-18
Author:  MXtremist
categories: 
tags:  [notes]
toc:  true
pinned:  true
music-type: "song"
music-id: 1354634080
comments:  true
--- 

在这里记录和分享我的搭建经验，~~应该不会~~持续更新

<!-- more -->

# 开始

想建自己的网站这个想法已经在我脑海里存留很久了，然而受限于服务器和域名的价格（~~贫穷~~）一直没有实现。偶然了解到[GitHub Pages](https://pages.github.com/)的存在之后，打算着手开始建立个人博客，可能会在这里发一些乱七八糟的东西。



# 搭建并完善

## 基于GitHub Pages搭建个人博客

关于基础的建立，可以参考[LOFFER使用基础教程](https://fromendworld.github.io/LOFFER/document/)，本站使用的模板完全基于LOFFER。教程中包括评论区的建立等内容都非常完善且易懂，即使没有提到的东西在 `_config,yml` 和作者仓库的[README](https://github.com/FromEndWorld/LOFFER/blob/master/README.md)中也有非常详尽的注释。本文仅会分享一些我个人对原始模板的个性化。如果你想要直接使用我的一些个性化设置，也欢迎Fork[我的仓库](https://github.com/MXtremist/mxtremist.github.io)。

按照作者的步骤，很容易就能顺利搭建好个人博客。注意在为仓库（Repository）命名时，建议命名为 `name.github.io `，例如我的仓库就命名为 `mxtremist.github.io` ，这样我的博客首页就会是[mxtremist.github.io](https://mxtremist.github.io/)。



## 属于自己的LOGO

大触可以直接跳过，自己画一个就OK了。

关于logo的制作，这里推荐一个我认为比较好用的网站：[DesignEvo](https://www.designevo.com/cn/) ，使用免费且有较多个性化选择，唯一的问题是不支持背景透明（也可能是我没看到），如果使用不规则的图形，比如我这样的，可能需要背景透明才会更好看，这里推荐一个Windows下好用的icon编辑软件[icoFX](https://icofx.ro/downloads.html)，这个软件是我当初在个性化Windows 10的时候发现的，改天我可能会写一个关于美化Win10的文章。

编辑好自己的logo和favicon（用于显示在浏览器角标）之后，需要上传到图床，这里推荐[SM.MS](https://sm.ms/)，这也是老牌图床了，在国内好用且免费。

![ImageURL](https://i.loli.net/2020/06/18/lDKINy6tHE23aMO.png)

上传好后点击Image URL，将图片链接粘贴到 `_config.yml` 中对应位置即可。注意对于任何的改动，可能都需要几分钟才能在自己的主页刷新，所以如果有需求可以考虑增加本地博客预览功能，具体实现请问搜索引擎。

ps：如果是Windows端浏览器，建议使用Ctrl+R强制刷新。



## 只支持微博，还有一大堆不存在的社交链接？

原生模板中的社交链接仅有微博、GitHub和那些不存在的网站，那么如何进行自定义呢？

根目录下 `/include/svg-icons` 对应各个链接及其SVG矢量图标，以bilibili为例，只需要它的个人主页格式为`https://space.bilibili.com/{{ site.footer-links.bilibili }}`，我们用CV大法新添几行代码，再把其中的`<path d=>` 修改为自己想要的SVG图片的相关内容即可。图标的大小最好为48x48 px。现在的问题是如何得到SVG图标，[这里](https://github.com/FortAwesome/Font-Awesome/tree/master/svgs/brands)可以找到大部分品牌的SVG素材，然而如果没有那你想要的呢？

首先问问搜索引擎，我在网上找到了很多在线将图片转为SVG格式的网站，但是绝大多数都是“假的”SVG，即采用`<image>`标签加上一个base64图片，而我们需要的是`<svg> + <path d=>`这样用path画出路线实现矢量缩放。最终，我找到了一个很方便的[网站](https://www.vectorizer.io/)。自己选好图标，上传，得到SVG相关参数，CV大法，搞定！搞定图标之后，还需要配置 `_config,yml` 文件。以bilibili为例，在`foot-links`中添加：

```css
footer-links: 
  weibo: xxxxxx # 请输入你的微博个性域名 
  bilibili: xxxxxx # 这里填主站空间后面的数字   
```

最终结果如下图，奇怪的硬币增加了！

·<img src="https://i.loli.net/2020/06/19/zweYi6o5yhadATJ.png"/>



## 添加搜索功能

如果有一天，我的博客写了成千上万篇，那么我该如何快速找到我想要的博客呢？归档和标签是一个好方法，但是如果同一个tag内依然有大量文章，或者不记得是哪一年的了呢？这时候就需要一个简单的搜索功能。

搜索功能由[Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search)提供技术支持。点击右上角donwload，解压后将`/example/js`文件夹和`/example/search.json`文件上传到我们自己的仓库根目录下即可。

接下来需要在想要显示的页面配置搜索框，例如想要在主页，那么就打开`index.html`，粘贴以下两端代码：

```css
<!--配置搜索框样式-->
<div class="search-container">
  <input type="text" id="search-input" placeholder="search..." style="
    width: 100%;
    height: 34px;
    color: #15aabf;
    background-color: rgba(180,242,245,.2);
    line-height: 32px;
    padding: 0px 16px;
    margin: 10px 0px;
    border: 1px solid #15aabf;
    border-radius: 17px;
    font-size: 16px;
    font-weight: bold;
    outline: none;
    box-sizing: border-box;
    box-shadow: inset 0 1px 1px rgba(0,0,0,.1), 0 0 12px rgba(21,170,191,.7);
    ">
  <ul id="results-container"></ul>
</div>
```

```css
<!--配置搜索功能-->
<script src="/js/simple-jekyll-search.min.js"></script>

<script>
	window.simpleJekyllSearch = new SimpleJekyllSearch({
	searchInput: document.getElementById('search-input'),
	resultsContainer: document.getElementById('results-container'),
	json: '/search.json',
	searchResultTemplate: '<li><a href="{url}?query={query}" title="{desc}">{title}</a></li>',
	limit: 5,
	fuzzy: false,
	exclude: ['Welcome']
  })
</script>
```

其中第一部分为配置搜索框样式，如果想要自定义，可以参考[CSS样式大全](https://www.cnblogs.com/laihuayan/archive/2012/07/27/2611111.html)。

搜索框最终实现效果如下图：

<img src="https://i.loli.net/2020/06/19/a6YgRhGi7rEt3pV.png"/>



## 那么有没有人看我的博客呢？

浏览量是衡量一个网站/一篇文章很重要的数据，那么有没有什么方便的工具呢？俗话说得好，*你不用 Google，你有 Bing...*

通过搜索发现，[这里](http://busuanzi.ibruce.info/)有一个非常简单好用的工具，有了它，我们就可以很方便地在想要的位置添加想要显示的数据。例如，在`index.html`的末尾添加：

```css
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
<div align="center">
	<span id="busuanzi_container_site_pv" style="font-family:Consolas;color:rgba(21,170,191,.6);font-size:12px;">
		Page View:<span id="busuanzi_value_site_pv" style="font-family:Consolas;color:Silver;font-size:12px;"></span>
	</span>
	<span id="busuanzi_container_site_uv" style="font-family:Consolas;color:rgba(21,170,191,.6);font-size:12px;">
		Vistor:<span id="busuanzi_value_site_uv" style="font-family:Consolas;color:Silver;font-size:12px;"></span>
	</span>
</div>
```

就可以显示主站的访问量（PV）和访问人数（UV），而在\_layouts/post.html的末尾添加：

```css
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
<div align="center">
	<span id="busuanzi_container_page_pv" style="font-family:Consolas;color:rgba(21,170,191,.6);font-size:12px;">
		本文阅读量:<span id="busuanzi_value_page_pv" style="font-family:Consolas;color:Silver;font-size:12px;"></span>
	</span>
</div>
```

就可以查看这篇文章的阅读量。这里是显示效果：

<img src="https://i.loli.net/2020/06/19/BJFc54oXneyUKhx.png"/>

显然，没什么人看我的博客XD。

除此之外还有配置Google Analytics的傻瓜式操作，这里不再赘述了。



## 音乐播放器来!

如果你想要为自己的网站添加音乐播放器，那么慎用浏览器搜索教程！因为网上的教程绝大多数基于网易云音乐生成的外链播放器，然而，出于未知原因，在2019年前后，网易云音乐大规模地停止了对外链播放器的支持，~~网易云biss！~~，那么我们还有其他的方法么？

经过我一个下午的寻找，终于找到了METO大佬的[MetingJS](https://github.com/metowolf/MetingJS)项目，该项目为我们提供了一个使用起来极其方便的音乐播放器插件。想要使用这个插件，首先我们在`_includes/`下创建文件`cloud-music.html`，填写下列代码：

```html
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

<meting-js
	server="netease"
	type={{ page.music-type }}
	id={{ page.music-id }}
	autoplay=true
	theme=#0b7285
	>
</meting-js>
```

关于meting-js内各个参数的意义，参考[MetingJS官方手册](https://github.com/metowolf/MetingJS/blob/master/README.md)以及[Aplayer官方手册](https://aplayer.js.org/#/zh-Hans/)。注意到我们还有`type`和`id`两项没有使用了参数，这个会在后面解释。

接下来，找到你需要添加音乐播放器的位置。例如，我想要在每篇文章的正文开头添加，就打开`_layouts/post.html`，找到正文开头位置：

```css
<div class="entry">
<!-- 这里是正文开头 -->
```

插入如下代码：(在每行前添加\{和% )

```css
if page.music-id %}
	in clude cloud-music.html %}
endif %} 
```

这样，我们的音乐播放器就实现好了，现在需要为其指定播放的歌曲。

在文章的`markdown`文件开头layout内添加变量music-type和music-id，前者可以为`song`, `playlist`, `album`, `search`, `artist`，指明播放类型，后者为id代码。以网易云音乐为例，如果我想要播放[Bloom](https://music.163.com/#/song?id=1354634080)这首歌，网址：https://music.163.com/#/song?id=1354634080，就添加：

```js
music-type: "song"
music-id: 1354634080
```

而如果我想要播放歌单，把music-type改为"playlist"，id改为歌单id即可。歌单id需要在网页版打开歌单查看网址。音乐播放器的效果如下图所示，可以说是非常的鹅妹子嘤啊：

<img src="https://i.loli.net/2020/06/19/eBV54iMRmIYFE3c.png"/>



## 其他自定义

| **修改属性** |      **文件位置**      |
| :----------: | :--------------------: |
|   主题颜色   | \_sass/_variables.scss |
|     主页     |       index.html       |
|    文章页    |  \_layouts/post.html   |
|   sidebar    |  \_includes/nav.html   |

本地预览：在根目录下执行命令`jekyll server`，然后访问`http://127.0.0.1:4000/`.



# 更新日志

## 2020-6-16

> 添加：
>
> - 个人博客正式上线
>
> - 支持基于Disqus的评论



## 2020-6-17

> 添加：
>
> - 现在支持bilibili链接了
>- 增加了搜索（仅支持搜索posts内文件名和tag）
> - 增加了访问人数统计
> 
> 修改：
> 
> - 替换了新的logo和favicon，自我感觉更好看了
> - 将评论区由Disqus替换为Gittalk，然而依然被墙



## 2020-6-18

> 修改：
>
> - 调整了搜索框的样式



## 2020-6-19

> 添加：
>
> - 添加了音乐播放器
>
> 修改：
>
> - 修改了主题颜色



# 致谢

- [Jekyll](https://github.com/jekyll/jekyll) - 这是本站存在的根基
- [LOFFER](https://github.com/FromEndWorld/LOFFER) - 提供了基础框架及教程
- [DesignEvo](https://www.designevo.com/cn/) - 在线制作免费好康的logo
- [vectorizer](https://www.vectorizer.io/) - 常见图片格式转换为真·SVG
- [SM.MS](https://sm.ms/) - 免费好用没被墙的图床
- [Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search) - 搜索功能支持
- [不蒜子](http://busuanzi.ibruce.info/) - 访问计数功能支持