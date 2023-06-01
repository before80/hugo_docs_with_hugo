+++
title = "Slice"
weight = 108
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# slice

[https://gohugo.io/functions/slice/](https://gohugo.io/functions/slice/)

Creates a slice (array) of all passed arguments.

## 语法

```
slice ITEM...
```

One use case is the concatenation of elements in combination with the [`delimit` function](https://gohugo.io/functions/delimit/):

slice.html



```go-html-template
{{ $sliceOfStrings := slice "foo" "bar" "buzz" }}
<!-- returns the slice [ "foo", "bar", "buzz"] -->
{{ delimit ($sliceOfStrings) ", " }}
<!-- returns the string "foo, bar, buzz" -->
```
