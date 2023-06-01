+++
title = "Path_Ext"
weight = 78
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Ext

[https://gohugo.io/functions/path.ext/](https://gohugo.io/functions/path.ext/)

Ext returns the file name extension of a path.

## 语法

```
path.Ext PATH
```

`path.Ext` returns the file name extension `PATH`.

The extension is the suffix beginning at the final dot in the final slash-separated element `PATH`; it is empty if there is no dot.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ path.Ext "a/b/c/news.html" }} → ".html"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Join](https://gohugo.io/functions/path.join/)
