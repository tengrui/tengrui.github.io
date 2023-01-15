---
layout: post
title:  "My First Blog!"
date:   2014-12-23 21:01:28
tag:    Jekyll
categories: SharePoint
---
今天终于搞了一个基于Github Pages和Jekyll的博客。以前在GAE里面搞过一个，但是不久就被墙了。

虽然我基本上不怎么写博客，但对技术的折腾精神还是有一点的。
简单总结一下搭建这种博客的过程吧。

1. 首先需要有个Github的账号。

2. 建立一个name.github.io的仓库，用来存放Jekyll Blog。

3. 安装Github Windows客户端，并clone之前建的这个仓库

4. 安装Ruby和Ruby的DevKit。安装DevKit的时候，可能需要自己改一下config.xml，在3个“-”下面增加引号里面的内容：

	“ - C:/Ruby21-x64”

5. 安装Bundler，国内用户可能需要添加一下source

	gem source -a http://ruby.taobao.org

6. 在本地仓库的根目录下，用Jekyll生成一个blog模板

	jekyll new .

7. 使用jekyll serve命令，就可以在本机预览blog的效果了

	http://localhost:4000/

8. 用客户端同步到Github上，就有了一个Jekyll的blog了。

9. 如果有自己的域名，添加CNAME项，并在Github仓库里添加一个CNAME文件，稍等片刻就可以看到自己的域名成了这个博客啦。
