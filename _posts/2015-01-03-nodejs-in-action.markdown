---
layout: post
title:  "《Node.js实战》学习笔记1"
date:   2015-01-03 21:01:28
tag:    Node.js
categories: SharePoint
---
应该是因为Bluemix的缘故，我一时兴起，打算学习Node.js搞一个自己的网站，然后就买了这本《Node.js实战》。和平常一样，粗略看了几页后，就束之高阁了。

直到最近，某网站的用户和密码泄露了，网上有人搞了一个网页，可供人们查询自己的邮箱是否在泄露名单之列。于是有了自己也搞一个想法。

想法虽然简单，但自己确实没有太多做网站的经验，连输入框、按钮都不知道怎么弄。几乎一切从零开始，HTML，CSS，Javascript，在这些都不熟悉的情况下，鼓捣Node.js。我想我当时也是醉了吧。

从Bluemix上面下载的模板用的是express，然后发现这本书的第8章也讲的是这个框架，于是直接从第8章开始啃。其实当时连什么是模板，什么是框架都一头雾水。

虽然一天时间就把功能实现了，但对Node.js却连入门都称不上。所以决定从头看一遍这本书。

另一个因素是新买了一个机械键盘，平时的使用量真是少啊，正好敲敲书上的代码，试试新键盘:P

搞了几天Javascript，也许是没找到好的编辑器的缘故，敲错代码后真的很难找啊。慢慢摸索吧，目前使用的是未注册的Sublime Text 2.

略有小成的是今天发现书上一处勘误。第49页的代码中：

    client.on('connect', function() {
      channel.emit('join', id, client);
    });

应改为：

    channel.emit('join', id, client);

因为这个client的‘connect’事件在走到这行代码前就发生了，所以这个事件在这里不可能捕捉到。

当然我是到网上搜到了相关的code，加上自己改完后实际运行才证实了这个想法。

网上的链接打不开，镜像的链接是：

http://cc.bingj.com/cache.aspx?q=nodejs+in+action+chapter+3&d=4702483785978640&mkt=zh-CN&setlang=zh-CN&w=FFkoDMnWDoBacSzD7d5wsuC-6-8xmUM-

当前进度：49页。