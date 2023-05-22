+++
title = "Reflect_IsMap"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# reflect.IsMap

[https://gohugo.io/functions/reflect.ismap/](https://gohugo.io/functions/reflect.ismap/)

Reports if a value is a map.

## 语法

```
reflect.IsMap INPUT
```

`reflect.IsMap` reports if `VALUE` is a map. Returns a boolean.

```go-html-template
{{ reflect.IsMap (dict "key" "value") }} → true
{{ reflect.IsMap "yo" }} → false
```

## 另请参阅

- [reflect.IsSlice](https://gohugo.io/functions/reflect.isslice/)
