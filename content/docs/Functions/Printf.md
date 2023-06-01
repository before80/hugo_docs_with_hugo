+++
title = "printf"
weight = 84
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# printf

[https://gohugo.io/functions/printf/](https://gohugo.io/functions/printf/)

Formats a string using the standard `fmt.Sprintf` function.

## 语法

```
printf FORMAT INPUT
```

See [the go doc](https://golang.org/pkg/fmt/) for additional information.

```go-html-template
{{ i18n ( printf "combined_%s" $var ) }}
{{ printf "formatted %.2f" 3.1416 }}
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
