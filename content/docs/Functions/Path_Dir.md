+++
title = "path.Dir"
weight = 77
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Dir

[https://gohugo.io/functions/path.dir/](https://gohugo.io/functions/path.dir/)

Dir returns all but the last element of a path.

## 语法

```
path.Dir PATH
```

`path.Dir` returns all but the last element of `PATH`, typically `PATH`’s directory.

The returned path will never end in a slash. If `PATH` is empty, `.` is returned.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ path.Dir "a/news.html" }} → "a"
{{ path.Dir "news.html" }} → "."
{{ path.Dir "a/b/c" }} → "a/b"
{{ path.Dir "/x/y/z" }} → "/x/y"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
- [path.Join](https://gohugo.io/functions/path.join/)
