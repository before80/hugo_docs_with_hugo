+++
title = "Chomp"
weight = 21
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# chomp

[https://gohugo.io/functions/chomp/](https://gohugo.io/functions/chomp/)

Removes any trailing newline characters.

## 语法

```
chomp INPUT
strings.Chomp INPUT
```

Useful in a pipeline to remove newlines added by other processing (e.g., [`markdownify`](https://gohugo.io/functions/markdownify/)).

```go-html-template
{{ chomp "<p>Blockhead</p>\n" }} → "<p>Blockhead</p>"
```
