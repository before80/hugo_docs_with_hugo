+++
title = "Print"
weight = 83
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# print

[https://gohugo.io/functions/print/](https://gohugo.io/functions/print/)

Prints the default representation of the given arguments using the standard `fmt.Print` function.

## 语法

```
print INPUT
```

See [the go doc](https://golang.org/pkg/fmt/) for additional information.

```go-html-template
{{ print "foo" }} → "foo"
{{ print "foo" "bar" }} → "foobar"
{{ print (slice 1 2 3) }} → [1 2 3]
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
