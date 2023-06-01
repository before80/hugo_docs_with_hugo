+++
title = "anchorize"
weight = 17
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# anchorize

[https://gohugo.io/functions/anchorize/](https://gohugo.io/functions/anchorize/)

Takes a string and sanitizes it the same way as the [`defaultMarkdownHandler`](https://gohugo.io/getting-started/configuration-markup#configure-markup) does for markdown headers.

## 语法

```
anchorize INPUT
```

If [Goldmark](https://gohugo.io/getting-started/configuration-markup#goldmark) is set as `defaultMarkdownHandler`, the sanitizing logic adheres to the setting [`markup.goldmark.parser.autoHeadingIDType`](https://gohugo.io/getting-started/configuration-markup#goldmark).

Since the `defaultMarkdownHandler` and this template function use the same sanitizing logic, you can use the latter to determine the ID of a header for linking with anchor tags.

```go-html-template
{{ anchorize "This is a header" }} --> "this-is-a-header"
{{ anchorize "This is also    a header" }} --> "this-is-also----a-header"
{{ anchorize "main.go" }} --> "maingo"
{{ anchorize "Article 123" }} --> "article-123"
{{ anchorize "<- Let's try this, shall we?" }} --> "--lets-try-this-shall-we"
{{ anchorize "Hello, 世界" }} --> "hello-世界"
```

## 另请参阅

- [.RenderString](https://gohugo.io/functions/renderstring/)
- [Content Formats](https://gohugo.io/content-management/formats/)
- [Markdown Render Hooks](https://gohugo.io/templates/render-hooks/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [emojify](https://gohugo.io/functions/emojify/)
