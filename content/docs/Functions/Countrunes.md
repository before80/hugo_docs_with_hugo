+++
title = "Countrunes"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# countrunes

[https://gohugo.io/functions/countrunes/](https://gohugo.io/functions/countrunes/)

Determines the number of runes in a string excluding any whitespace.

## 语法

```
countrunes INPUT
strings.CountRunes INPUT
```

In contrast with `countwords` function, which counts every word in a string, the `countrunes` function determines the number of runes in the content and excludes any whitespace. This has specific utility if you are dealing with CJK-like languages.

```go-html-template
{{ "Hello, 世界" | countrunes }}
<!-- outputs a content length of 8 runes. -->
```

## 另请参阅

- [countwords](https://gohugo.io/functions/countwords/)
- [strings.Count](https://gohugo.io/functions/strings.count/)
- [strings.RuneCount](https://gohugo.io/functions/strings.runecount/)
