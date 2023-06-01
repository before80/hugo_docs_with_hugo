+++
title = "Path_Clean"
weight = 76
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# path.Clean

[https://gohugo.io/functions/path.clean/](https://gohugo.io/functions/path.clean/)

Replaces path separators with slashes (`/`) and removes extraneous separators.

## 语法

```
path.Clean PATH
```

`path.Clean` replaces path separators with slashes (`/`) and removes extraneous separators, including trailing separators.

```go-html-template
{{ path.Clean "foo//bar" }} → "foo/bar"
{{ path.Clean "/foo/bar/" }} → "/foo/bar"
```

On a Windows system, if `.File.Path` is `foo\bar.md`, then:

```go-html-template
{{ path.Clean .File.Path }} → "foo/bar.md"
```

## 另请参阅

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
- [path.Dir](https://gohugo.io/functions/path.dir/)
- [path.Ext](https://gohugo.io/functions/path.ext/)
- [path.Join](https://gohugo.io/functions/path.join/)
