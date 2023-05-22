+++
title = "Countwords"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# countwords

[https://gohugo.io/functions/countwords/](https://gohugo.io/functions/countwords/)

Counts the number of words in a string.

## 语法

```
countwords INPUT
```

The template function works similar to the [.WordCount page variable](https://gohugo.io/variables/page/).

```go-html-template
{{ "Hugo is a static site generator." | countwords }}
<!-- outputs a content length of 6 words.  -->
```

## 另请参阅

- [countrunes](https://gohugo.io/functions/countrunes/)
- [strings.Count](https://gohugo.io/functions/strings.count/)
- [strings.RuneCount](https://gohugo.io/functions/strings.runecount/)
