+++
title = "Shuffle"
weight = 105
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# shuffle

[https://gohugo.io/functions/shuffle/](https://gohugo.io/functions/shuffle/)

Returns a random permutation of a given array or slice.

## 语法

```
shuffle COLLECTION
{{ shuffle (seq 1 2 3) }} → [3 1 2] 
{{ shuffle (slice "a" "b" "c") }} → [b a c] 
```

The result will vary from one build to the next.

## 另请参阅

- [sort](https://gohugo.io/functions/sort/)
