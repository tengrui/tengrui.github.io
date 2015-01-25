---
layout: post
title:  "《Node.js实战》学习笔记5"
date:   2015-01-21 22:38:00
tag:    Node.js
categories: SharePoint
---
看Express的时候问题更多了，主要是因为Node变化太快了。

有些问题找到了解决方法，比如8.1.2节在生成框架的时候，首先需要安装一下express-generator

    npm install -g express-generator

等生成了框架，模板里面的内容变化也很大，而且运行的方式也不同。书上写的是运行"node app.js"，但现在的框架需要运行的是：

    node ./bin/www

第8章被卡住问题是8.4.2节的bodyParser和multipart中间件不工作，因为这个中间件可能也移出了express。记得曾经解决了这个问题，可惜没有记录下来，先不研究了。

后续的章节就大体浏览了一下，这本书就算看完了吧。