+++
title = ".Render"
weight = 9
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Render

[https://gohugo.io/functions/render/](https://gohugo.io/functions/render/)

​	应用视图来渲染内容。

## 语法

```
.Render LAYOUT
```

​	该视图是一种替代布局，应该是一个文件名，指向 [内容视图](https://gohugo.io/templates/views) 文档中指定位置之一的模板。 

​	此函数仅适用于 [列表上下文](https://gohugo.io/templates/lists/) 中的单个内容。

​	例如，下面的示例可以使用位于  `/layouts/_default/summary.html`  中的内容视图来渲染一篇内容：

```go-html-template
{{ range .Pages }}
  {{ .Render "summary" }}
{{ end }}
```

## 另请参阅

- [Content View Templates](https://gohugo.io/templates/views/)
