+++
title = "FileExists"
weight = 35
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# fileExists

[https://gohugo.io/functions/fileexists/](https://gohugo.io/functions/fileexists/)

Checks for file or directory existence.

## 语法

```
os.FileExists PATH
fileExists PATH
```

The `os.FileExists` function attempts to resolve the path relative to the root of your project directory. If a matching file or directory is not found, it will attempt to resolve the path relative to the [`contentDir`](https://gohugo.io/getting-started/configuration#contentdir). A leading path separator (`/`) is optional.

With this directory structure:

```text
content/
├── about.md
├── contact.md
└── news/
    ├── article-1.md
    └── article-2.md
```

The function returns these values:

```go-html-template
{{ os.FileExists "content" }} --> true
{{ os.FileExists "content/news" }} --> true
{{ os.FileExists "content/news/article-1" }} --> false
{{ os.FileExists "content/news/article-1.md" }} --> true
{{ os.FileExists "news" }} --> true
{{ os.FileExists "news/article-1" }} --> false
{{ os.FileExists "news/article-1.md" }} --> true
```
