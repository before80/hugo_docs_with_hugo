+++
title = "Sha"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# sha

[https://gohugo.io/functions/sha/](https://gohugo.io/functions/sha/)

Hashes the given input and returns either an SHA1 or SHA256 checksum.

## 语法

```
sha1 INPUT
sha256 INPUT
```

`sha1` hashes the given input and returns its SHA1 checksum.

```go-html-template
{{ sha1 "Hello world, gophers!" }}
<!-- returns the string "c8b5b0e33d408246e30f53e32b8f7627a7a649d4" -->
```

`sha256` hashes the given input and returns its SHA256 checksum.

```go-html-template
{{ sha256 "Hello world, gophers!" }}
<!-- returns the string "6ec43b78da9669f50e4e422575c54bf87536954ccd58280219c393f2ce352b46" -->
```

## 另请参阅

- [hmac](https://gohugo.io/functions/hmac/)
