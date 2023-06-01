+++
title = "Plainify"
weight = 81
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# plainify

[https://gohugo.io/functions/plainify/](https://gohugo.io/functions/plainify/)

Strips any HTML and returns the plain text version of the provided string.

## 语法

```
plainify INPUT
{{ "<b>BatMan</b>" | plainify }} → "BatMan"
```

See also the `.PlainWords`, `.Plain`, and `.RawContent` [page variables](https://gohugo.io/variables/page/).

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
