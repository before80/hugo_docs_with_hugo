+++
title = "strings.TrimLeft"
weight = 121
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.TrimLeft

[https://gohugo.io/functions/strings.trimleft/](https://gohugo.io/functions/strings.trimleft/)

Returns a slice of a given string with all leading characters contained in the cutset removed.

## 语法

```
strings.TrimLeft CUTSET STRING
```

Given the string `"abba"`, leading `"a"`’s can be removed a follows:

```
{{ strings.TrimLeft "a" "abba" }} → "bba"
```

Numbers can be handled as well:

```
{{ strings.TrimLeft 12 1221341221 }} → "341221"
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
