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

## 开始

想建自己的网站这个想法已经在我脑海里存留很久了，然而受限于服务器和域名的价格（~~贫穷~~）一直没有实现。偶然了解到[GitHub Pages](https://pages.github.com/)的存在之后，打算着手开始建立个人博客，可能会在这里发一些乱七八糟的东西。



## 搭建并完善

### 基于GitHub Pages搭建个人博客

关于基础的建立，可以参考[LOFFER使用基础教程](https://fromendworld.github.io/LOFFER/document/)，本站使用的模板完全基于LOFFER。教程中包括评论区的建立等内容都非常完善且易懂，即使没有提到的东西在 `_config,yml` 和作者仓库的[README](https://github.com/FromEndWorld/LOFFER/blob/master/README.md)中也有非常详尽的注释。本文仅会分享一些我个人对原始模板的个性化。如果你想要直接使用我的一些个性化设置，也欢迎Fork[我的仓库](https://github.com/MXtremist/mxtremist.github.io)。

按照作者的步骤，很容易就能顺利搭建好个人博客。注意在为仓库（Repository）命名时，建议命名为 `name.github.io `，例如我的仓库就命名为 `mxtremist.github.io` ，这样我的博客首页就会是[mxtremist.github.io](https://mxtremist.github.io/)。



### 属于自己的LOGO

大触可以直接跳过，自己画一个就OK了。

关于logo的制作，这里推荐一个我认为比较好用的网站：[DesignEvo](https://www.designevo.com/cn/) ，使用免费且有较多个性化选择，唯一的问题是不支持背景透明（也可能是我没看到），如果使用不规则的图形，比如我这样的，可能需要背景透明才会更好看，这里推荐一个Windows下好用的icon编辑软件[icoFX](https://icofx.ro/downloads.html)，这个软件是我当初在个性化Windows 10的时候发现的，改天我可能会写一个关于美化Win10的文章。

编辑好自己的logo和favicon（用于显示在浏览器角标）之后，需要上传到图床，这里推荐[SM.MS](https://sm.ms/)，这也是老牌图床了，在国内好用且免费。

![ImageURL](https://i.loli.net/2020/06/18/lDKINy6tHE23aMO.png)

上传好后点击Image URL，将图片链接粘贴到 `_config.yml` 中对应位置即可。注意对于任何的改动，可能都需要几分钟才能在自己的主页刷新，所以如果有需求可以考虑增加本地博客预览功能，具体实现请问搜索引擎。

ps：如果是Windows端浏览器，建议使用Ctrl+R强制刷新。



### 只支持微博，还有一大堆不存在的社交链接？

原生模板中的社交链接仅有微博、GitHub和那些不存在的网站，那么如何进行自定义呢？

根目录下 `/include/svg-icons` 对应各个链接及其SVG矢量图标，以bilibili为例，只需要它的个人主页格式为`https://space.bilibili.com/{{ site.footer-links.bilibili }}`，我们用CV大法新添几行代码，再把其中的`<path d=>` 修改为自己想要的SVG图片的相关内容即可。图标的大小最好为48x48 px。现在的问题是如何得到SVG图标，[这里](https://github.com/FortAwesome/Font-Awesome/tree/master/svgs/brands)可以找到大部分品牌的SVG素材，然而如果没有那你想要的呢？

首先问问搜索引擎，我在网上找到了很多在线将图片转为SVG格式的网站，但是绝大多数都是“假的”SVG，即采用`<image>`标签加上一个base64图片，而我们需要的是`<svg> + <path d=>`这样用path画出路线实现矢量缩放。最终，我找到了一个很方便的[网站](https://www.vectorizer.io/)。搞定图标之后，还需要配置 `_config,yml` 文件。以bilibili为例，在`foot-links`中添加：

```css
footer-links: 
  weibo: xxxxxx # 请输入你的微博个性域名 
  bilibili: xxxxxx # 这里填主站空间后面的数字   
```



### 添加搜索功能

如果有一天，我的博客写了成千上万篇，那么我该如何快速找到我想要的博客呢？归档和标签是一个好方法，但是如果同一个tag内依然有大量文章，或者不记得是哪一年的了呢？这时候就需要一个简单的搜索功能。

搜索功能由[Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search)提供技术支持。点击右上角donwload，解压后将`/example/js`文件夹和`/example/search.json`文件上传到我们自己的仓库根目录下即可。

接下来需要在想要显示的页面配置搜索框，例如想要在主页，那么就打开`index.html`，粘贴以下两端代码：

```css
<!--配置搜索框样式-->
<div class="search-container">
  <input type="text" id="search-input" placeholder="search blog posts..." style="
    width: 100%;
    height: 34px;
    color: #109599;
    background-color: rgba(239,242,245,.2);
    line-height: 32px;
    padding: 0px 16px;
    margin: 4px 1px;
    border: 1px solid #109599;
    border-radius: 17px;
    font-size: 16px;
    font-weight: bold;
    outline: none;
    box-sizing: border-box;
    box-shadow: inset 0 1px 1px rgba(0,0,0,.1), 0 0 12px rgba(16,149,113,.7);
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



## 更新日志

> 2020-6-16

添加：

- 个人博客正式上线
- 支持基于Disqus的评论



> 2020-6-17

添加：

- 现在支持bilibili链接了
- 增加了搜索（仅支持搜索posts内文件名和tag）
- 增加了访问人数统计

修改：

- 替换了新的logo和favicon，自我感觉更好看了
- 将评论区由Disqus替换为Gittalk，然而依然被墙



> 2020-6-18

修改：

- 调整了搜索框的样式



## 致谢

- [Jekyll](https://github.com/jekyll/jekyll) - 这是本站存在的根基
- [LOFFER](https://github.com/FromEndWorld/LOFFER) - 提供了基础框架及教程
- [DesignEvo](https://www.designevo.com/cn/) - 在线制作免费好康的logo
- [vectorizer](https://www.vectorizer.io/) - 常见图片格式转换为真·SVG
- [SM.MS](https://sm.ms/) - 免费好用没被墙的图床
- [Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search) - 搜索功能支持
- [不蒜子](http://busuanzi.ibruce.info/) - 访问计数功能支持