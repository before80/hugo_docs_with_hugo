+++
title = "页面方法"
weight = 4
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Pages Methods - 页面方法 

[https://gohugo.io/variables/pages/](https://gohugo.io/variables/pages/)

​	Pages是Hugo中的核心页面集合，具有许多有用的方法。

​	此外，请参阅[列表模板](https://gohugo.io/templates/lists)以获取排序方法的概述。

## .Next PAGE 

​	在`Pages`上的`.Next`和`.Prev`与在`.Page`上具有相同名称的方法类似，但更加灵活（并且略微慢一些），因为它们可以用于任何页面集合。

​	`.Next`指向与作为参数发送的页面相对的下一个页面。例如：`{{ with .Site.RegularPages.Next . }}{{ .RelPermalink }}{{ end }}`。对集合中的第一个页面调用`.Next`将返回`nil`。

## .Prev PAGE 

​	`.Prev`指向与作为参数发送的页面相对的上一个页面。例如：`{{ with .Site.RegularPages.Prev . }}{{ .RelPermalink }}{{ end }}`。对集合中的最后一个页面调用`.Prev`将返回`nil`。

## 另请参阅  

- [页面变量](https://gohugo.io/variables/page/)
