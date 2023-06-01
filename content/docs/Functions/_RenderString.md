+++
title = ".RenderString"
weight = 10
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .RenderString

[https://gohugo.io/functions/renderstring/](https://gohugo.io/functions/renderstring/)

​	将标记渲染为 HTML。  

## 语法

```
.RenderString MARKUP
```

​	`.RenderString`  是  `Page`  上的方法，它使用为该页面定义的内容渲染器（如果选项中未设置）将一些标记渲染为 HTML。  

​	该方法带有一个可选的 map 参数，其中包含以下选项：  

- display ("inline")

  `inline` or `block`. If `inline` (default), surrounding `<p></p>` on short snippets will be trimmed.

  `inline`  或  `block` 。如果是  `inline` （默认值），则会在简码片段周围修剪  `<p></p>` 。  

- markup (defaults to the Page’s markup)

  请参见[内容格式列表](https://gohugo.io/content-management/formats/#list-of-content-formats)中的标识符。 

以下是一些示例：

```go-html-template
{{ $optBlock := dict "display" "block" }}
{{ $optOrg := dict "markup" "org" }}
{{ "**Bold Markdown**" | $p.RenderString }}
{{ "**Bold Block Markdown**" | $p.RenderString  $optBlock }}
{{ "/italic org mode/" | $p.RenderString  $optOrg }}
```

[自 v0.93.0 开始使用](https://github.com/gohugoio/hugo/releases/tag/v0.93.0) **注意**：[markdownify](https://gohugo.io/functions/markdownify/) 使用此函数以支持 [Render Hooks](https://gohugo.io/getting-started/configuration-markup/#markdown-render-hooks)。 

## 另请参阅

- [Content Formats](https://gohugo.io/content-management/formats/)
- [Markdown Render Hooks](https://gohugo.io/templates/render-hooks/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [markdownify](https://gohugo.io/functions/markdownify/)
