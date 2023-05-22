+++
title = "Strings_TrimPrefix"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.TrimPrefix

[https://gohugo.io/functions/strings.trimprefix/](https://gohugo.io/functions/strings.trimprefix/)

Returns a given string s without the provided leading prefix string. If s doesn’t start with prefix, s is returned unchanged.

## 语法

```
strings.TrimPrefix PREFIX STRING
```

Given the string `"aabbaa"`, the specified prefix is only removed if `"aabbaa"` starts with it:

```
{{ strings.TrimPrefix "a" "aabbaa" }} → "abbaa"
{{ strings.TrimPrefix "aa" "aabbaa" }} → "bbaa"
{{ strings.TrimPrefix "aaa" "aabbaa" }} → "aabbaa"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
