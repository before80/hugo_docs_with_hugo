+++
title = "Symdiff"
weight = 126
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# symdiff

[https://gohugo.io/functions/symdiff/](https://gohugo.io/functions/symdiff/)

`collections.SymDiff` (alias `symdiff`) returns the symmetric difference of two collections.

## 语法

```
COLLECTION | symdiff COLLECTION
```

Example:

```go-html-template
{{ slice 1 2 3 | symdiff (slice 3 4) }}
```

The above will print `[1 2 4]`.

Also see https://en.wikipedia.org/wiki/Symmetric_difference

## 另请参阅

- [intersect](https://gohugo.io/functions/intersect/)
- [union](https://gohugo.io/functions/union/)
- [append](https://gohugo.io/functions/append/)
- [complement](https://gohugo.io/functions/complement/)
- [group](https://gohugo.io/functions/group/)
