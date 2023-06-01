+++
title = "path.Join"
weight = 79
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Join

[https://gohugo.io/functions/path.join/](https://gohugo.io/functions/path.join/)

Join path elements into a single path.

## 语法

```
path.Join ELEMENT...
```

`path.Join` joins path elements into a single path, adding a separating slash if necessary. All empty strings are ignored.

**Note:** All path elements on Windows are converted to slash (’/’) separators.

```go-html-template
{{ path.Join "partial" "news.html" }} → "partial/news.html"
{{ path.Join "partial/" "news.html" }} → "partial/news.html"
{{ path.Join "foo/baz" "bar" }} → "foo/baz/bar"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [path.Clean](https://gohugo.io/functions/path.clean/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
