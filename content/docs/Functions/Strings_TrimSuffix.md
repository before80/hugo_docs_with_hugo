+++
title = "Strings_TrimSuffix"
weight = 124
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.TrimSuffix

[https://gohugo.io/functions/strings.trimsuffix/](https://gohugo.io/functions/strings.trimsuffix/)

Returns a given string s without the provided trailing suffix string. If s doesn’t end with suffix, s is returned unchanged.

## 语法

```
strings.TrimSuffix SUFFIX STRING
```

Given the string `"aabbaa"`, the specified suffix is only removed if `"aabbaa"` ends with it:

```
{{ strings.TrimSuffix "a" "aabbaa" }} → "aabba"
{{ strings.TrimSuffix "aa" "aabbaa" }} → "aabb"
{{ strings.TrimSuffix "aaa" "aabbaa" }} → "aabbaa"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
