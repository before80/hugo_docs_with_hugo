+++
title = "Strings_Contains"
weight = 113
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# strings.Contains

[https://gohugo.io/functions/strings.contains/](https://gohugo.io/functions/strings.contains/)

Reports whether a string contains a substring.

## 语法

```
strings.Contains STRING SUBSTRING
{{ strings.Contains "Hugo" "go" }} → true
```

The check is case sensitive:

```
{{ strings.Contains "Hugo" "Go" }} → false
```
