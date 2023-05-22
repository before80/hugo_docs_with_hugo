+++
title = "Truncate"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# truncate

[https://gohugo.io/functions/truncate/](https://gohugo.io/functions/truncate/)

Truncates a text to a max length without cutting words or leaving unclosed HTML tags.

## 语法

```
truncate SIZE [ELLIPSIS] INPUT
strings.Truncate SIZE [ELLIPSIS] INPUT
```

Since Go templates are HTML-aware, `truncate` will intelligently handle normal strings vs HTML strings:

```go-html-template
{{ "<em>Keep my HTML</em>" | safeHTML | truncate 10 }}` → <em>Keep my …</em>`
```

If you have a raw string that contains HTML tags you want to remain treated as HTML, you will need to convert the string to HTML using the [`safeHTML` template function](https://gohugo.io/functions/safehtml/) before sending the value to truncate. Otherwise, the HTML tags will be escaped when passed through the `truncate` function.

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
