---
category: blog
published: false
layout: post
title: "天作之和: github pages + prose.io"
description: github jekyll静态页面自动生成，沉浸式的书写体验，git版本控制，夫复何求？
---

## Why github pages + prose.io？

一句话：**github jekyll静态页面自动生成，沉浸式的书写体验，git版本控制，夫复何求？**

写Blog是一个很随意的行为，通常人们对写得要求也不高，所以从WordPress到轻博客再到微博，写的是越来越轻，越来越容易。

但是维护Blog并不容易。

对于向我这样的人来说，一个可以维护的Blog系统需要

1. 用简单的数据格式存储
> 想要找到某片Blog的文章时，无需翻箱倒柜将后台数据库大卸八块。Come on，blog本来不应该就是些txt文件么？Grep一把为什么就不行？

2. 有一个沉浸式的编写工具
> 这个很重要。写东西的时候总是需要没有干扰，左右两边不要不停的有“齐x短裙热卖9元起”这样的东西飞来飞去。

3. 能打草稿，能版本控制。
> 人就是这么懒，想起来一点写一点，但是如果有个工具激励，事情或许会不同一点。

所以github pages是个貌似理想的选择：存储就是文本文件，加上一点简单Markdown；版本控制用git，没有更好的了。

但是github pages缺少一个简单的编写工具。或者说，没有一个简单的可以在Web上使用的工具。clone到本地，动用jekyll server再加vim，显得太重量，适合做一些比较有创造性的事情，不适合随便写写。

于是prose.io弥补了这个空缺，提供了一个很好的在线github pages编辑工具，问题解决了。

## 看起来怎样

以你现在看到的这个blog为例吧，看起来是这样的

![LI, Yu from 1981](/images/github-prose-start.png)

点击左上角的Edit之后，进入在线编辑器，是这样的

![Editing _posts-blog-2014-03-25-github-prose-blog.md](/images/github-prose-edit1.png)

完成编写，提交是这样的
![Editing _posts-blog-2014-03-25-github-prose-blog.md](/images/github-prose-edit2.png)

点击完毕提交，boom，commit到github，github pages通过hook就自动生成了静态页面，就这么简单。

当然，因为它是github pages，所以clone，vim随便写一个很复杂的演示什么的都很容易，无比强大。

想备份，git clone，想观察更改记录，github的web界面就[可以用](https://github.com/liyu1981/liyu1981.github.io/commits/master/_posts/blog/2014-03-25-github-prose-blog.md)。

总之，如果你是程序猿，没有比这个更加合适的了。

## 怎样弄一个

基本上，包含两个步骤

1. 弄好一个jekyll设置好的github pages
2. 设置好prose.io

### 设置好github pages

怎样设置好github pages，再把jekyll配置好，教程已有不少，比如[这个](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)，还有[这个](http://sanvibyfish.github.io/posts/githubpage/)，以及我参考的[这个](http://beiyuu.com/github-pages/)。

看起来都很简单，实际上做起来往往又不是那么尽如人意，你懂得。

> 老湿，能不能再给力一点？copy paste如何？

这个要求不是不可以满足，如果实在对个性化没什么要求，这儿有个123的方案

1. 我准备了一个模板，[fork它](https://github.com/liyu1981/template-githubio/fork)
> 首先当然你要有一个github账号，没有也没有关系，会提示你创建的。

2. 去github界面上把repo的名字改成 <你的名字>.github.io 
> github修改repo名字就是在repo页面上点那个setting，第一个选项卡就有。这里[有图有真相](https://help.github.com/articles/renaming-a-repository)。

3. 修改一下repo根目录下_config.yml里面myblog组下的一些信息

| Key | 说明 |
|---------|--------------------|
| gavatar | 你email地址的md5值，用于模板里gavatar头像显示。给个[在线计算工具](http://md5-hash-online.waraxe.us/)，注意全用小写 |
| gpname | github账号的名字 |
| linkedin | linkedin链接 |
| github | github链接 |
| coverimgs | index页右侧的背景图数组，替换下http那部分，没有就留个`[]` |
| postbgimg | blog post页的背景图url |

做人不是很讲究的话，这就算是搞完了（当然，美化这种事情是永恒的，我懂得，以后随意改）

### 设置prose.io

不用prose.io，直接在github的online edit也是可以的，prose.io提供了一个稍好的编辑环境，所以可以一试。

prose.io总的来说没什么配置的，不配置也行，直接访问[http://prose.io](http://prose.io) ，授权就行了。

如果要配置，基本上就是在_config.yml里面添加一些个prose.io用的配置，基本上可以[参考这里](https://github.com/prose/prose/wiki/Prose-Configuration)。

如果是从我给的模板fork的，那就不用修改了，已经配置好了。

## Prose.io使用上的注意事项

1. Prose.io的markdown默认不显示jekyll metadata，需要点击右边的对应button显示和编辑。

2. 配置了jekyll之后，prose.io默认的标题就不在是`xxxx-xx-xx-yyy-zzz.md`这样的格式，而是做为真正的title。英文的习惯下，commit到github的文件名会将这个title拆字后用`-`组合形成文件名，例如`hello world`最后会组合成`2014-03-27-hello-world`这样。使用中文的情况下，这个机制就不怎么灵光了。所以如果要避免生成一些`2014-03-27-.md`这样的名字，先在title里面用英文关键字写，commit，然后再修改成中文。这样就行。

3. 如果用我模板里面的配置，prose.io里面的文章默认是unpublished，所以大可以慢慢写完再说，要发布的时候点击工具栏转成published，再commit就会自动生成。

4. prose.io当前支持插入图片，会自动上传到github里面（在_config.yml里面配置）。但是太过于彪悍的文件名，比如很黄很暴力的，很多火星文的，有中国特色中文的，都会导致各种各样的问题。因此，为了世界和平，拖进去之前还是自己改个人畜无伤的名字吧。