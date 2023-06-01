+++
title = "Reflect_IsSlice"
weight = 92
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# reflect.IsSlice

[https://gohugo.io/functions/reflect.isslice/](https://gohugo.io/functions/reflect.isslice/)

Reports if a value is a slice.

## 语法

```
reflect.IsSlice INPUT
```

`reflect.IsSlice` reports if `VALUE` is a slice. Returns a boolean.

```go-html-template
{{ reflect.IsSlice (slice 1 2 3) }} → true
{{ reflect.IsSlice "yo" }} → false
```

## 另请参阅

- [reflect.IsMap](https://gohugo.io/functions/reflect.ismap/)
