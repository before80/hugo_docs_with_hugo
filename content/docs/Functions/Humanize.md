+++
title = "Humanize"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# humanize

[https://gohugo.io/functions/humanize/](https://gohugo.io/functions/humanize/)

Returns the humanized version of an argument with the first letter capitalized.

## 语法

```
humanize INPUT
```

If the input is either an int64 value or the string representation of an integer, humanize returns the number with the proper ordinal appended.

```go-html-template
{{ humanize "my-first-post" }} → "My first post"
{{ humanize "myCamelPost" }} → "My camel post"
{{ humanize "52" }} → "52nd"
{{ humanize 103 }} → "103rd"
```

## 另请参阅

- [lower](https://gohugo.io/functions/lower/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
