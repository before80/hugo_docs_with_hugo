+++
title = "Replace"
weight = 96
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# replace

[https://gohugo.io/functions/replace/](https://gohugo.io/functions/replace/)

Replaces all occurrences of the search string with the replacement string.

## 语法

```
replace INPUT OLD NEW [LIMIT]
strings.Replace INPUT OLD NEW [LIMIT]
```

Replace returns a copy of `INPUT` with all occurrences of `OLD` replaced with `NEW`. The number of replacements can be limited with an optional `LIMIT` parameter.

```
`{{ replace "Batman and Robin" "Robin" "Catwoman" }}`
→ "Batman and Catwoman"

{{ replace "aabbaabb" "a" "z" 2 }} → "zzbbaabb"
```
