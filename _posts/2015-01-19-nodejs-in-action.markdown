---
layout: post
title:  "《Node.js实战》学习笔记4"
date:   2015-01-19 21:24:00
tag:    Node.js
categories: SharePoint
---
看完了Connect框架及其中间件的使用。

但是Connect的中间件已经发生了变化，所以第7章的内容已经有点问题，那些中间件都独立了，不再属于Connect。比如原来的connect.cookieParser已经变成了cookie-parser。可以用下面的方法安装

    npm install cookie-parser

另外在Windows下的curl命令，Cookie是用分号分隔的，而不是书上的逗号。例如：

    curl http://localhost:3000/ -H "Cookie: foo=bar; bar=baz"

测试签名cookie的时候，遇到了问题，服务器不能解析签名的cookie，试了SHA-1，SHA-256，MD5等方式的签名，都没有办法通过服务器的验证。后果就是后面的章节也没心情看了，第七章简单浏览了一下，顺手还提了一个勘误。、

如果显示地安装老版本的connect，也许就能测试一下书上的示例了，不过现在已经开始看第8章，当前进度：160页。