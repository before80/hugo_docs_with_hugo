+++
title = "SafeCSS"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# safeCSS

[https://gohugo.io/functions/safecss/](https://gohugo.io/functions/safecss/)

Declares the provided string as a known "safe" CSS string.

## 语法

```
safeCSS INPUT
```

In this context, *safe* means CSS content that matches any of the following:

1. The CSS3 stylesheet production, such as `p { color: purple }`.
2. The CSS3 rule production, such as `a[href=~"https:"].foo#bar`.
3. CSS3 declaration productions, such as `color: red; margin: 2px`.
4. The CSS3 value production, such as `rgba(0, 0, 255, 127)`.

Example: Given `style = "color: red;"` defined in the front matter of your `.md` file:

- `<p style="{{ .Params.style | safeCSS }}">…</p>` → `<p style="color: red;">…</p>`
- `<p style="{{ .Params.style }}">…</p>` → `<p style="ZgotmplZ">…</p>`

"ZgotmplZ" is a special value that indicates that unsafe content reached a CSS or URL context.

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
