---
layout: post
title:  "《Node.js实战》学习笔记2"
date:   2015-01-07 22:39:00
tag:    Node.js
categories: SharePoint
---
最近还是继续看书和敲代码。

第四章开始讲RESTful Web服务了，我的理解就是用GET，POST，PUT和DELETE来进行CRUD操作。更详细的解释可以参考下面的链接，包括一些设计的常见误区。

[理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)

为了测试RESTful，这里需要一个cURL工具，我下载了一个Windows上的[cURL](http://www.paehl.com/open_source/downloads/curl_X64_ssl.7z)。

各个HTTP谓词的命令分别为：

    POST: curl -d “item1” http://localhost:3000
    GET: curl http://localhost3000
    DELETE: curl -X DELETE http://localhost:3000/1
    PUT: curl -X PUT http://localhost:3000/1?item2

在DELETE的基础上，简单实现了PUT谓词：

        case 'PUT':
            var path = url.parse(req.url).pathname;
            var i = parseInt(path.slice(1), 10);
            var item = url.parse(req.url).query;

            console.log(item);
            if (isNaN(i)) {
                res.statusCode = 400;
                res.end('Invalid item id');
            } else if (!items[i]) {
                res.statusCode = 404;
                res.end('Item not found');
            } else {
                items[i] = item;
                res.end('OK\n');
            }
            break;

最近听说了一些关于Node.js的负面评价，有人还搞出了fibjs，能更好地支持串行编程。不过我还是想先熟悉一下Node.js，另外还打算研究一下网络爬虫，并用Node.js实现一个。感觉这个东西用并行更好一点吧。

当前进度：73页。