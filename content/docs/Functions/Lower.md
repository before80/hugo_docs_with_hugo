+++
title = "Lower"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# lower

[https://gohugo.io/functions/lower/](https://gohugo.io/functions/lower/)

Converts all characters in the provided string to lowercase.

## 语法

```
lower INPUT
strings.ToLower INPUT
```

Note that `lower` can be applied in your templates in more than one way:

```go-html-template
{{ lower "BatMan" }} → "batman"
{{ "BatMan" | lower }} → "batman"
```

## 另请参阅

- [humanize](https://gohugo.io/functions/humanize/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
