+++
title = "strings.ContainsAny"
weight = 114
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.ContainsAny

[https://gohugo.io/functions/strings.containsany/](https://gohugo.io/functions/strings.containsany/)

Reports whether a string contains any character from a given string.

## 语法

```
strings.ContainsAny STRING CHARACTERS
{{ strings.ContainsAny "Hugo" "gm" }} → true
```

The check is case sensitive:

```
{{ strings.ContainsAny "Hugo" "Gm" }} → false
```
