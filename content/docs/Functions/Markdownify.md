+++
title = "Markdownify"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# markdownify

[https://gohugo.io/functions/markdownify/](https://gohugo.io/functions/markdownify/)

Renders markdown to HTML.

## 语法

```
markdownify INPUT
{{ .Title | markdownify }}
```

If the resulting HTML is a single paragraph, Hugo removes the wrapping `p` tags to produce inline HTML as required per the example above.

To keep the wrapping `p` tags for a single paragraph, use the [`.Page.RenderString`](https://gohugo.io/functions/renderstring/) method, setting the `display` option to `block`.

If the resulting HTML is two or more paragraphs, Hugo leaves the wrapping `p` tags in place.

Although the `markdownify` function honors [markdown render hooks](https://gohugo.io/templates/render-hooks/) when rendering markdown to HTML, use the `.Page.RenderString` method instead of `markdownify` if a render hook accesses `.Page` context. See issue [#9692](https://github.com/gohugoio/hugo/issues/9692) for details.

## 另请参阅

- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [.RenderString](https://gohugo.io/functions/renderstring/)
- [Build Options](https://gohugo.io/content-management/build-options/)
- [Comments](https://gohugo.io/content-management/comments/)
- [Content Formats](https://gohugo.io/content-management/formats/)
