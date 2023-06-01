+++
title = "last"
weight = 61
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# last

[https://gohugo.io/functions/last/](https://gohugo.io/functions/last/)

slices an array to only the last Nth elements.

## 语法

```
last INDEX COLLECTION
{{ range last 10 .Pages }}
  {{ .Render "summary" }}
{{ end }}
```
