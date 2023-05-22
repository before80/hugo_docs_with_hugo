+++
title = "Path_BaseName"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.BaseName

[https://gohugo.io/functions/path.basename/](https://gohugo.io/functions/path.basename/)

BaseName returns the last element of a path, removing the extension if present.

## 语法

```
path.BaseName PATH
```

If `PATH` is empty, `.` is returned.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ path.BaseName "a/news.html" }} → "news"
{{ path.BaseName "news.html" }} → "news"
{{ path.BaseName "a/b/c" }} → "c"
{{ path.BaseName "/x/y/z/" }} → "z"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [Base Templates and Blocks](https://gohugo.io/templates/base/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
