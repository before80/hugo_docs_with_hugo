+++
title = "append"
weight = 18
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# append

[https://gohugo.io/functions/append/](https://gohugo.io/functions/append/)

`append` appends one or more values to a slice and returns the resulting slice.

## 语法

```
COLLECTION | append VALUE [VALUE]...
COLLECTION | append COLLECTION
```

An example appending single values:

```go-html-template
{{ $s := slice "a" "b" "c" }}
{{ $s = $s | append "d" "e" }}
{{/* $s now contains a []string with elements "a", "b", "c", "d", and "e" */}}
```

The same example appending a slice to a slice:

```go-html-template
{{ $s := slice "a" "b" "c" }}
{{ $s = $s | append (slice "d" "e") }}
```

The `append` function works for all types, including `Pages`.

## 另请参阅

- [complement](https://gohugo.io/functions/complement/)
- [group](https://gohugo.io/functions/group/)
- [intersect](https://gohugo.io/functions/intersect/)
- [symdiff](https://gohugo.io/functions/symdiff/)
- [union](https://gohugo.io/functions/union/)
