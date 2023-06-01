+++
title = "ReadDir"
weight = 88
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# readDir

[https://gohugo.io/functions/readdir/](https://gohugo.io/functions/readdir/)

Returns an array of FileInfo structures sorted by filename, one element for each directory entry.

## 语法

```
os.ReadDir PATH
readDir PATH
```

The `os.ReadDir` function resolves the path relative to the root of your project directory. A leading path separator (`/`) is optional.

With this directory structure:

```text
content/
├── about.md
├── contact.md
└── news/
    ├── article-1.md
    └── article-2.md
```

This template code:

```go-html-template
{{ range os.ReadDir "content" }}
  {{ .Name }} --> {{ .IsDir }}
{{ end }}
```

Produces:

```html
about.md --> false
contact.md --> false
news --> true
```

Note that `os.ReadDir` is not recursive.

Details of the `FileInfo` structure are available in the [Go documentation](https://pkg.go.dev/io/fs#FileInfo).

For more information on using `readDir` and `readFile` in your templates, see [Local File Templates](https://gohugo.io/templates/files).

## 另请参阅

- [File Variables](https://gohugo.io/variables/files/)
- [Local File Templates](https://gohugo.io/templates/files/)
- [os.Stat](https://gohugo.io/functions/os.stat/)
- [readFile](https://gohugo.io/functions/readfile/)
