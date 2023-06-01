+++
title = "split"
weight = 111
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# split

[https://gohugo.io/functions/split/](https://gohugo.io/functions/split/)

Returns a slice of strings by splitting STRING by DELIM.

## 语法

```
split STRING DELIM
```

Examples:

```go-html-template
{{ split "tag1,tag2,tag3" "," }} → ["tag1", "tag2", "tag3"]
{{ split "abc" "" }} → ["a", "b", "c"]
```

`split` essentially does the opposite of [delimit](https://gohugo.io/functions/delimit). While `split` creates a slice from a string, `delimit` creates a string from a slice.

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
