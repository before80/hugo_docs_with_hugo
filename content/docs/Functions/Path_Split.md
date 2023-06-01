+++
title = "Path_Split"
weight = 80
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Split

[https://gohugo.io/functions/path.split/](https://gohugo.io/functions/path.split/)

Split path immediately following the final slash.

## 语法

```
path.Split PATH
```

`path.Split` splits `PATH` immediately following the final slash, separating it into a directory and a base component.

The returned values have the property that `PATH` = `DIR`+`BASE`. If there is no slash in `PATH`, it returns an empty directory and the base is set to `PATH`.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ $dirFile := path.Split "a/news.html" }} → $dirFile.Dir → "a/", $dirFile.File → "news.html"
{{ $dirFile := path.Split "news.html" }} → $dirFile.Dir → "", $dirFile.File → "news.html"
{{ $dirFile := path.Split "a/b/c" }} → $dirFile.Dir → "a/b/", $dirFile.File →  "c"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
