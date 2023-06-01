+++
title = "Md5"
weight = 68
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# md5

[https://gohugo.io/functions/md5/](https://gohugo.io/functions/md5/)

hashes the given input and returns its MD5 checksum.

## 语法

```
md5 INPUT
{{ md5 "Hello world, gophers!" }}
<!-- returns the string "b3029f756f98f79e7f1b7f1d1f0dd53b" -->
```

This can be useful if you want to use [Gravatar](https://en.gravatar.com/) for generating a unique avatar:

```html
<img src="https://www.gravatar.com/avatar/{{ md5 "your@email.com" }}?s=100&d=identicon">
```
