+++
title = "strings.Count"
weight = 115
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.Count

[https://gohugo.io/functions/strings.count/](https://gohugo.io/functions/strings.count/)

Returns the number of non-overlapping instances of a substring within a string.

## 语法

```
strings.Count SUBSTR STRING
```

If `SUBSTR` is an empty string, this function returns 1 plus the number of Unicode code points in `STRING`.

| Example                                 | Result |
| :-------------------------------------- | :----- |
| `{{ "aaabaab" | strings.Count "a" }}`   | 5      |
| `{{ "aaabaab" | strings.Count "aa" }}`  | 2      |
| `{{ "aaabaab" | strings.Count "aaa" }}` | 1      |
| `{{ "aaabaab" | strings.Count "" }}`    | 8      |

## 另请参阅

- [strings.RuneCount](https://gohugo.io/functions/strings.runecount/)
- [countrunes](https://gohugo.io/functions/countrunes/)
- [countwords](https://gohugo.io/functions/countwords/)
