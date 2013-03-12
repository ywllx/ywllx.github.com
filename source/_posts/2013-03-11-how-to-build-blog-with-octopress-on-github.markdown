---
layout: post
title: "利用octopress在github构建自己的博客"
date: 2013-03-11 22:26
comments: true
categories: octopress github
---
早就想着自己动手利用github搭建一个能自己控制的博客，上个周末，终于把想法变成行动了，google了一把之后，打开了[一篇文章](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)，介绍如何利用github Pages和Jekyll搭建一个免费的，无限流量的Blog，这不正是我所需要的吗！但是对jekll并不熟，文章也没有详细介绍如何利用它。继续google，发现了octopress这个工具，而且网上对介绍如何利用它搭建博客的文章很多，于是参考这些文章，开始搭建自己的博客了。下面则主要是这个过程的一个简单记录。

---
#### 一些准备
搭建博客主要用到了下面这些技术和工具，首先对它们进行一些简单的介绍：

* [Github](http://pages.github.com/)：GitHub 是一个用于使用Git版本控制系统项目的共享虚拟主机服务。它由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner使用Ruby on Rails编写而成。GitHub同时提供付费账户和为开源项目提供的免费账户。Git是一个分布式的版本控制系统，最初由Linus Torvalds编写，用作Linux内核代码的管理。在推出后，Git在其它项目中也取得了很大成功。有人把github比作程序员中的facebook，在上面，我们可以很容易构建自己的开源项目。
这里搭建博客主要用到了了Github的Pages功能，它允许用户自定义项目首页。github Pages可以被认为是用户编写的、托管在github上的静态网页，而且它还支持域名绑定。Github Pages同时提供了模板功能，可以用解析引擎是Jekyll。
* [Jekyll](http://jekyllrb.com/): Jekyll是一个简单的免费的Blog生成工具，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，不需要数据库，文章可以使用Markdown、HTML、Textile格式的文件保存。Jekyll只是一个生成静态网页的工具，可以配合第三方服务，例如disqus。而且jekyll可以免费部署在Github上，可以绑定自己的域名。
* [Octopress](http://octopress.org/)：Octopress是由Brandon Mathis设计的针对Jekyll的框架，使用Jekyll你可以DIY你个人博客的每一部分,但是你可能就得自己编写自己的HTML模板，CSS，javascript脚本。这对于大多数人来说可能还是太复杂繁琐，那么你可以使用Octopress，它有一系列便捷的命令负责生成、预览、发布、新建文章、新建页面等等，有本地预览功能，有一套还算美观的模版，这个模板修改起来还是很方便的，网站源码和静态页面分离。可以在git以不同分支管理。这样你便可以轻松搭建一个自己的博客。
* [Markdown](http://zh.wikipedia.org/wiki/Markdown)：Markdown 是一种轻量级标记语言，创始人为John Gruber和Aaron Swartz。它允许人们“使用易读易写的纯文本格式编写文档， 然后转换成有效的XHTML(或者HTML)文档”。这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。 Github的README.md文件就是用Markdown格式写的。在这里了解[Markdown基本语法](http://wowubuntu.com/markdown/#p)，简单学习你就可以使用它写博客了。

---
#### 如何搭建
知道搭建博客主要用到的工具后，搭建一个基本的博客就很简单了，[这篇文章](http://xuhehuan.com/783.html)则详细介绍了在windows环境下搭建博客的详细步骤，在linux环境下基本过程也差不多，另外Octopress的[官方文档](http://octopress.org/docs/)也有详细的介绍。完成这些操作后你应该得到如下图所示的一个博客。
<img src=/images/version0.JPEG title="初始博客">

---
#### 个性化设置
完成上述步骤后，在/octopress目录下，你首先可以执行`rake new_post["Title"]`命令，这条命令会在source/_post目录下生存一个以日期开头的后缀为.markdown的文件，利用你喜欢的编辑器，按照markdown语法编辑此文件，然后执行`rake generate`,`rake deploy`命令就可以生成你的一篇新博客。但凡是使用Octopress搭建的博客，如果不再做修改，那么风格将会是一样的，而且功能单一，下面则将介绍做一些简单的修改，将它进行一点个性化的设置。

*更改背景颜色与正文字体*

在Octopress安装完成之后，在sass/custom/下面有一些特殊的文件，根据命名可以猜到它是用来设置你的博客字体，颜色，布局的配置文件，这些配置文件一般会在最后载入。我们将它做一些修改，就可以对你博客的背景色，字体，布局等做出你个性化的设置。这里我参考[这个博客](http://aijazansari.com/2012/08/27/how-to-customize-octopress-theme/)修改_colors.scss文件如下：
```scss
html {
   background: #d8d8d8 !important;
 }
 body {
   > div {
     background: #fff !important;
     > div {
       background: #fff !important;
       }
   }
}
$main-bg: #ffffff!default;
$page-bg: #ffffff !default;
  
$header-bg: #81BEF7;
$subtitle-color: lighten($header-bg, 58);
$nav-bg: desaturate(lighten(#8fc17a, 18), 5);
$nav-bg-front: image-url('noise.png');
$nav-bg-back: linear-gradient(lighten($nav-bg, 8), $nav-bg, darken($nav-bg, 11));
$sidebar-bg: desaturate(#eceff5, 8);
$sidebar-link-color: saturate(#526f9a, 10);
$sidebar-link-color-hover: darken(#7ab662, 9);
$footer-bg: #ccc !default;
$footer-bg-front: image-url('noise.png');
$footer-bg-back: linear-gradient(lighten($footer-bg, 8), $footer-bg, darken($footer-bg, 11));
```
参考[这个博客](http://melandri.net/2012/02/14/octopress-theme-customization/)修改样式配置文件_styles.scss文件如下：
``` scss
body { font-size: 1em; }
body > div { background-image: none; }
body > div > div { background-image: none; }

/* ----- Content ----- */
#content .blog-index article h1 {
    font-size: 1.8em;
    font-weight: normal;
}

#content .blog-index article h1, #content .blog-index article h1 a, article header h1, article header h1 a{
    color: #555555 !important;
}

h1 { font-size: 1.8em; }

h1 span{
    font-weight: normal;
    color: #E0841B;
}

article h2, article h3, article header h1{
    font-weight: normal;
}

.blog-index article h1 a:hover{ text-decoration: none; }

article p {
    text-align:justify;
    margin-bottom: 1em;
}
```
*导航栏修改*

 实际上导航栏，标题等的修改都可通过编辑 /source/_includes/custom/里的每个文件来更新你的博客，具体可以参考[这篇博客](http://yanping.me/cn/blog/2012/01/07/theming-and-customization/)或者[官方文档](http://octopress.org/docs/)，这里不再详述，需要注意的一点是每个链接的href都以 {{ root_url }}开始 (如果网站部署到子目录里，这可以帮助Octopress采用不同的链接). 如果你想把你的网站部署到像 yoursite.com/octopress 这样的子目录，你必须把它加到你添加的任何链接里。例如我在_includes/custom/navigation.html增加了如下一行代码：
 ``` 
 <li><a href="{{ root_url }}/blog/about">关于</a></li>
 ```
 则需要在/blog/目录下新建一个about目录，然后下面新建了一个index.html文件，当你点击`关于本人`这个导航时连接到此html构建的网页。

*增加分享和评论*

是否希望自己的博客能被大家分享呢，或者希望能够和自己博客的读者有所互动，Octopress本身是默认带有国外facebook，twitter的分享功能的插件的，而且也带有Disqus评论功能插件，但一则因为墙的原因，二则为了真正地接地气，我们可以自己加入中国本地化的类似功能的插件，首先在/source/_includes/post目录下修改sharing.html文件如下：(目前不知道为什么，在octopress中输入{ %的方式都会进行代码解析，所以上面的{ %都进行了添加了来取消，在实际文章中输入的时候，将取消掉）
```
{_% if site.share_and_comment %}
{_% include post/share_and_comment.html %}
{_% endif %}
```
然后到[加网](http://www.jiathis.com/)和[友言](http://www.uyan.cc/)分别获得分享代码和评论代码（如下），放入新建的share_and_comment.html的文件中，将此文件存放在/source/_includes/post目录下
``` html
<!-- JiaThis Button BEGIN -->
<div class="jiathis_style_24x24">
    <a class="jiathis_button_qzone"></a>
    <a class="jiathis_button_tsina"></a>
    <a class="jiathis_button_tqq"></a>
    <a class="jiathis_button_renren"></a>
    <a class="jiathis_button_kaixin001"></a>
    <a href="http://www.jiathis.com/share" class="jiathis jiathis_txt jtico jtico_jiathis" target="_blank"></a>
    <a class="jiathis_counter_style"></a>
</div>
<script type="text/javascript" src="http://v3.jiathis.com/code/jia.js?uid=1357227497148830" charset="utf-8"></script>
<!-- JiaThis Button END -->

<!-- UY BEGIN -->
<div id="uyan_frame"></div>
<script type="text/javascript" id="UYScript" src="http://v1.uyan.cc/js/iframe.js?UYUserId=0" async=""></script>
<!-- UY END -->
```
最后修改_config.yml文件，设置share_and_comment为true，如下：
```
share_and_comment: true
```

*增加文章分类标签*

我们利用rake new_post["Title"]`命令生成一个新的博客markdown文件之后，一般来说开头会默认包含以下几行代码：
```
layout: post
title: "利用octopress在github构建自己的博客"
date: 2013-03-11 22:26
comments: true
categories: octopress github
```
其中categories便是你对这篇文章的分类标签，如何利用这些标签，找到我们想看的文章，便可以利用以下插件实现，具体参考的博客文章我一时找不到了，对原作者先表示抱歉。首先在plugins新建一个ruby文件category_list_tag.rb，增加一下代码：
```ruby
module Jekyll
  class CategoryListTag < Liquid::Tag
    def render(context)
      html = ""
      categories = context.registers[:site].categories.keys
      categories.sort.each do |category|
        posts_in_category = context.registers[:site].categories[category].size
        category_dir = context.registers[:site].config['category_dir']
        category_url = File.join(category_dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase)
        html << "<li class='category'><a href='/#{category_url}/'>#{category} (#{posts_in_category})</a></li>\n"
      end 
      html
    end 
  end 
end

Liquid::Template.register_tag('category_list', Jekyll::CategoryListTag)
```

然后在/source/_includes/asides/目录下新建category_list.html文件，增加以下代码（记得去掉{_%中的_）：

```html
<section>
  <h1>文章分类</h1>
  <ul id="categories">
    {_% category_list %}
  </ul>
</section>
```
在_config.yml中增加相关设置
```ruby
default_asides: [asides/recent_posts.html, asides/category_list.html]
```

*侧栏增加微博秀*

1. 首先到先到[微博秀](http://weibo.com/tool/weiboshow)里面生成自己的微博秀嵌入代码，找出最后的uid和verifier
2. 新建一个weiboxiu.html放置到source/_includes/asides下
```html 
 <section>  
  <ul id="weibo">  
    <li>  
	  (此处拷入微博秀生成的html代码）
    </li>  
  </ul>  
</section>   
```  
3. 在_config.yml中增加相关设置
```ruby
default_asides: [asides/recent_posts.html, asides/category_list.html, asides/weiboxiu.html]  
```

#### 结束感言
首先先介绍一个实用的方法，那就是当你想删掉某篇博客时，应该采用[这篇文章](http://wywon.com/blog/2012/07/08/octopress-github/)介绍的方法，首先删除相应的markdown文件，然后把source分支里相应的文件也删除，可以使用下面命令：
```
git add -u
git commit -m 'delete post'
git push origin source
```
至此，我的第一篇博客算完成了，花的时间几乎跟搭建这个博客花的时间一样多，深深感叹，要想像黑客一样写博客玩酷写博客可真不容易啊，真是辛苦。。。熬了几个晚上。。。
