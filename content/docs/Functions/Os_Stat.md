+++
title = "Os_Stat"
weight = 72
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# os.Stat

[https://gohugo.io/functions/os.stat/](https://gohugo.io/functions/os.stat/)

Returns a FileInfo structure describing a file or directory.

## 语法

```
os.Stat PATH
```

The `os.Stat` function attempts to resolve the path relative to the root of your project directory. If a matching file or directory is not found, it will attempt to resolve the path relative to the [`contentDir`](https://gohugo.io/getting-started/configuration#contentdir). A leading path separator (`/`) is optional.

```go-html-template
{{ $f := os.Stat "README.md" }}
{{ $f.IsDir }}    --> false (bool)
{{ $f.ModTime }}  --> 2021-11-25 10:06:49.315429236 -0800 PST (time.Time)
{{ $f.Name }}     --> README.md (string)
{{ $f.Size }}     --> 241 (int64)

{{ $d := os.Stat "content" }}
{{ $d.IsDir }}    --> true (bool)
```

Details of the `FileInfo` structure are available in the [Go documentation](https://pkg.go.dev/io/fs#FileInfo).

## 另请参阅

- [File Variables](https://gohugo.io/variables/files/)
- [Local File Templates](https://gohugo.io/templates/files/)
- [readDir](https://gohugo.io/functions/readdir/)
- [readFile](https://gohugo.io/functions/readfile/)
