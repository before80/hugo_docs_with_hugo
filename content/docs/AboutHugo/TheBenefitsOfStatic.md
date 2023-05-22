+++
title = "静态站点生成器的好处"
weight = 5
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# The Benefits of Static Site Generators - 静态站点生成器的好处

https://gohugo.io/about/benefits/

​	改进的性能、安全性和易用性是静态站点生成器如此吸引人的几个原因之一。

​	站点生成器的目的是将内容渲染成HTML文件。大多数都是"动态站点生成器"。这意味着HTTP服务器——即将文件发送到浏览器以供查看的程序——在每次终端用户请求页面时运行生成器创建一个新的HTML文件。

​	随着时间的推移，动态站点生成器被编程以缓存其HTML文件，以防止向终端用户提供页面时不必要的延迟。缓存的页面是网页的静态版本。

​	Hugo在缓存方面更进了一步，所有HTML文件都在您的计算机上渲染。您可以在将文件复制到托管HTTP服务器的计算机之前在本地查看这些文件。由于HTML文件不是动态生成的，我们称Hugo是一个静态站点生成器。

​	这有许多好处。最明显的是性能。HTTP服务器非常擅长发送文件——事实上，您可以使用动态站点所需内存和CPU的一小部分有效地提供相同数量的页面。

## 更多关于静态站点生成器的信息

- ["静态站点生成器简介"，David Walsh](https://davidwalsh.name/introduction-static-site-generators) 
- ["Hugo与WordPress页面加载速度比较：Hugo远胜WordPress"，GettingThingsTech](https://gettingthingstech.com/hugo-vs.-wordpress-page-load-speed-comparison-hugo-leaves-wordpress-in-its-dust/) 
- ["静态站点生成器"，O’Reilly](https://github.com/gohugoio/hugoDocs/files/1242701/static-site-generators.pdf) 
- [StaticGen: 顶级开源静态站点生成器（GitHub Stars）](https://www.staticgen.com/) 
- ["前十名静态站点生成器"，Netlify博客](https://www.netlify.com/blog/2016/05/02/top-ten-static-website-generators/) 
- ["The Resurgence of Static"，dotCMS](https://dotcms.com/blog/post/the-resurgence-of-static)

## 另请参阅

- [partialCached](https://gohugo.io/functions/partialcached/)