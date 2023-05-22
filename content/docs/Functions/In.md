+++
title = "In"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# in

[https://gohugo.io/functions/in/](https://gohugo.io/functions/in/)

Checks if an element is in an array or slice–or a substring in a string—and returns a boolean.

## 语法

```
in SET ITEM
```

The elements supported are strings, integers and floats, although only float64 will match as expected.

In addition, `in` can also check if a substring exists in a string.

```go-html-template
{{ if in .Params.tags "Git" }}Follow me on GitHub!{{ end }}
{{ if in "this string contains a substring" "substring" }}Substring found!{{ end }}
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
