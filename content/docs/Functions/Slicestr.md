+++
title = "slicestr"
weight = 109
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# slicestr

[https://gohugo.io/functions/slicestr/](https://gohugo.io/functions/slicestr/)

Creates a slice of a half-open range, including start and end indices.

## 语法

```
slicestr STRING START [END]
strings.SliceString STRING START [END]
```

For example, 1 and 4 creates a slice including elements 1 through 3. The `end` index can be omitted; it defaults to the string’s length.

- `{{ slicestr "BatMan" 3 }}` → "Man"
- `{{ slicestr "BatMan" 0 3 }}` → "Bat"

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
