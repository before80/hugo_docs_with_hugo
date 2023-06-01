+++
title = "Println"
weight = 85
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# println

[https://gohugo.io/functions/println/](https://gohugo.io/functions/println/)

Prints the default representation of the given argument using the standard `fmt.Print` function and enforces a linebreak.

## 语法

```
println INPUT
```

See [the go doc](https://golang.org/pkg/fmt/) for additional information. `\n` denotes the linebreak but isn’t printed in the templates as seen below:

```go-html-template
{{ println "foo" }} → "foo\n"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
