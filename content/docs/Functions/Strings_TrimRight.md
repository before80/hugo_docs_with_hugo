+++
title = "strings.TrimRight"
weight = 123
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.TrimRight

[https://gohugo.io/functions/strings.trimright/](https://gohugo.io/functions/strings.trimright/)

Returns a slice of a given string with all trailing characters contained in the cutset removed.

## 语法

```
strings.TrimRight CUTSET STRING
```

Given the string `"abba"`, trailing `"a"`’s can be removed a follows:

```
{{ strings.TrimRight "a" "abba" }} → "abb"
```

Numbers can be handled as well:

```
{{ strings.TrimRight 12 1221341221 }} → "122134"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
