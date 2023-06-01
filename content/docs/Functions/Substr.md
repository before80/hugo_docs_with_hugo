+++
title = "substr"
weight = 125
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# substr

[https://gohugo.io/functions/substr/](https://gohugo.io/functions/substr/)

Extracts parts of a string from a specified character’s position and returns the specified number of characters.

## 语法

```
substr STRING START [LENGTH]
strings.Substr STRING START [LENGTH]
```

It normally takes two parameters: `start` and `length`. It can also take one parameter: `start`, i.e. `length` is omitted, in which case the substring starting from start until the end of the string will be returned.

To extract characters from the end of the string, use a negative start number.

If `length` is given and is negative, that number of characters will be omitted from the end of string.

```go-html-template
{{ substr "abcdef" 0 }} → "abcdef"
{{ substr "abcdef" 1 }} → "bcdef"

{{ substr "abcdef" 0 1 }} → "a"
{{ substr "abcdef" 1 1 }} → "b"

{{ substr "abcdef" 0 -1 }} → "abcde"
{{ substr "abcdef" 1 -1 }} → "bcde"

{{ substr "abcdef" -1 }} → "f"
{{ substr "abcdef" -2 }} → "ef"

{{ substr "abcdef" -1 1 }} → "f"
{{ substr "abcdef" -2 1 }} → "e"

{{ substr "abcdef" -3 -1 }} → "de"
{{ substr "abcdef" -3 -2 }} → "d"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
