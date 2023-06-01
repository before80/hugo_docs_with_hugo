+++
title = "Delimit"
weight = 28
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# delimit

[https://gohugo.io/functions/delimit/](https://gohugo.io/functions/delimit/)

Loops through any array, slice, or map and returns a string of all the values separated by a delimiter.

## 语法

```
delimit COLLECTION DELIMITER [LAST]
```

Delimit a slice:

```go-html-template
{{ $s := slice "b" "a" "c" }}
{{ delimit $s ", " }} → "b, a, c"
{{ delimit $s ", " " and "}} → "b, a and c"
```

Delimit a map:

The `delimit` function sorts maps by key, returning the values.

```go-html-template
{{ $m := dict "b" 2 "a" 1 "c" 3 }}
{{ delimit $m ", " }} → "1, 2, 3"
{{ delimit $m ", " " and "}} → "1, 2 and 3"
```

## 另请参阅

- [.Scratch](https://gohugo.io/functions/scratch/)
- [after](https://gohugo.io/functions/after/)
- [first](https://gohugo.io/functions/first/)
- [range](https://gohugo.io/functions/range/)
