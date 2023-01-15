---
layout: post
title:  "编译JDK9"
date:   2015-04-05 14:40:00
tag:    Java
categories: SharePoint
---
最近翻出《深入理解Java虚拟机》宝典，打算深入学习一下Java。

第一章就遇到了问题，最后一节是“实战：自己编译JDK”。虽然感觉这么做的意义并不大，但还是本着“纸上得来终觉浅”的精神，打算实际尝试一下。

而实事也和书上介绍的一样，在Linux或Solaris上构建OpenJDK，要比在Windows平台上轻松许多。

![press](http://tengrui.github.io/public/upload/linux_jdk9.jpg)

不到长城非好汉，既然作者都亲自尝试了，我也来尝试一下吧。


1. 安装Visual Studio C++ 2010（英文版），以及SP1
2. 安装Cygwin，以及缺少的工具，比如diffutils，wget等
3. 安装hg，即Mercurial。在Windows和Cygwin中安装均可，但我最终成功的那次是使用Cygwin里面的版本。
4. 下载JDK 9源码，鉴于国内的网络环境，这个步骤可能需要很长时间，甚至失败。
	
	hg clone http://hg.openjdk.java.net/jdk9/jdk9/
	bash ./get_sourcesh

5. 在Cygwin里面下载并解压FreeType。

	wget http://download.savannah.gnu.org/releases/freetype/freetype-2.5.3.tar.gz
	tar -xzf freetype-2.5.3.tar.gz

6. 设置环境变量,保证VC在Cygwin的路径之前，取消JAVA_HOME等。

	export PATH="/cygdrive/c/Program Files (x86)/Microsoft Visual Studio 10.0/VC/bin":$PATH
	export -n JAVA_HOME
	export TMP=C:\\Windows\\TEMP
	export TEMP=C:\\Windows\\TEMP

7. 运行./configure，其中freetype的目录，msvcr100.dll的路径均根据实际情况，其中msvcr100.dll是从C:\Windows\SysWOW64里面拷贝出来的。

	bash ./configure --with-freetype-src=/cygdrive/d/OpenJDK/freetype-2.5.3 --with-msvcr-dll="/cygdrive/c/Windows/SysWOW64/msvcr100.dll" --with-target-bits=32

8. 运行make all

	make all

经历了2个多小时的编译，虽然中间好像有些警告，另外运行的时候也有一个错误外，终于把JDK9在Windows上编译出来了。

![press](http://tengrui.github.io/public/upload/java_version.jpg)