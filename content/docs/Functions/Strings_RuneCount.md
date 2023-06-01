+++
title = "Strings_RuneCount"
weight = 120
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.RuneCount

[https://gohugo.io/functions/strings.runecount/](https://gohugo.io/functions/strings.runecount/)

Determines the number of runes in a string.

## 语法

```
strings.RuneCount INPUT
```

In contrast with `strings.CountRunes` function, which strips HTML and whitespace before counting runes, `strings.RuneCount` simply counts all the runes in a string. It relies on the Go [`utf8.RuneCountInString`] function.

```go-html-template
{{ "Hello, 世界" | strings.RuneCount }}
<!-- outputs a content length of 9 runes. -->
```

## 另请参阅

- [strings.Count](https://gohugo.io/functions/strings.count/)
- [countrunes](https://gohugo.io/functions/countrunes/)
- [countwords](https://gohugo.io/functions/countwords/)
- [len](https://gohugo.io/functions/len/)
