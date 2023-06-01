+++
title = "Upper"
weight = 137
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# upper

[https://gohugo.io/functions/upper/](https://gohugo.io/functions/upper/)

Converts all characters in a string to uppercase

## 语法

```
upper INPUT
strings.ToUpper INPUT
```

Note that `upper` can be applied in your templates in more than one way:

```go-html-template
{{ upper "BatMan" }} → "BATMAN"
{{ "BatMan" | upper }} → "BATMAN"
```
