---
layout: post
title:  "《Java程序员修炼之道》学习笔记1"
date:   2015-01-25 23:49:00
tag:    Java
categories: SharePoint
---
最近开始看《Java程序员修炼之道》。从副标题和简介来看，主要是介绍Java 7新特性，以及JVM上其他语言的应用，如Groovy、Scala和Clojure。

已经看完了第一部分，了解了一下Coin项目和NIO.2（在《Core Java》中，将其与Java 1.4引入的NIO相对比，称之为“新新IO”）。

首先，Coin项目包含的是Java语言特性的微小改动，共6个新特性：

1. switch语句中的String
2. 更强的数值文本表示法
3. 改善后的异常处理
4. TWR（try-with-resources）
5. 钻石语法
6. 简化变参方法调用

总的来说这些语法都很方便有用。

其次，NIO.2中引入了Path、Files和WatchService等类，据说比原来的File类更方便。

但是对于实际项目，尤其是我目前参与项目来说，首先要升级到Java 7的JRE，然后再考虑要不要重构以前的代码。由于现有代码可能已经实现了Path的这些功能，以及出于稳定性的考虑，一般是没有机会重写相关的代码的。

另外，本书有配套的代码，下载后的编译可能会遇到一些问题，其中之一和Scala与Java 8的版本冲突有关（因为本地JDK已经升级到Java 8），可以把pom.xml中Scala的版本修从‘2.9.0’改为‘2.10.2’来解决。

      <!-- Scala compiler plugin -->
      <plugin>
        <groupId>org.scala-tools</groupId>
        <artifactId>maven-scala-plugin</artifactId>
        <version>2.14.1</version>
        <executions>
          <execution>
            <goals>
              <goal>compile</goal>
              <goal>testCompile</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <scalaVersion>2.10.2</scalaVersion>
        </configuration>
      </plugin>

虽然改完了还是有其他的问题，但相比这个都比较容易解决。