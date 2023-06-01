+++
title = "readFile"
weight = 89
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# readFile

[https://gohugo.io/functions/readfile/](https://gohugo.io/functions/readfile/)

Returns the contents of a file.

## 语法

```
os.ReadFile PATH
readFile PATH
```

The `os.ReadFile` function attempts to resolve the path relative to the root of your project directory. If a matching file is not found, it will attempt to resolve the path relative to the [`contentDir`](https://gohugo.io/getting-started/configuration#contentdir). A leading path separator (`/`) is optional.

With a file named README.md in the root of your project directory:

```text
This is **bold** text.
```

This template code:

```go-html-template
{{ os.ReadFile "README.md" }}
```

Produces:

```html
This is **bold** text.
```

Note that `os.ReadFile` returns raw (uninterpreted) content.

For more information on using `readDir` and `readFile` in your templates, see [Local File Templates](https://gohugo.io/templates/files).

## 另请参阅

- [File Variables](https://gohugo.io/variables/files/)
- [Local File Templates](https://gohugo.io/templates/files/)
- [os.Stat](https://gohugo.io/functions/os.stat/)
- [readDir](https://gohugo.io/functions/readdir/)
