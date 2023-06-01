+++
title = "path.Base"
weight = 74
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Base

[https://gohugo.io/functions/path.base/](https://gohugo.io/functions/path.base/)

Base returns the last element of a path.

## 语法

```
path.Base PATH
```

`path.Base` returns the last element of `PATH`.

If `PATH` is empty, `.` is returned.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ path.Base "a/news.html" }} → "news.html"
{{ path.Base "news.html" }} → "news.html"
{{ path.Base "a/b/c" }} → "c"
{{ path.Base "/x/y/z/" }} → "z"
```

## 另请参阅

- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [Base Templates and Blocks](https://gohugo.io/templates/base/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
