+++
title = "crypto.FNV32a"
weight = 26
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# crypto.FNV32a

[https://gohugo.io/functions/crypto.fnv32a/](https://gohugo.io/functions/crypto.fnv32a/)

Returns the FNV (Fowler–Noll–Vo) 32 bit hash of a given string.

## 语法

```
crypto.FNV32a STRING
```

This function calculates the 32 bit [FNV1a hash](https://en.wikipedia.org/wiki/Fowler–Noll–Vo_hash_function#FNV-1a_hash) of a given string according to the [specification](https://datatracker.ietf.org/doc/html/draft-eastlake-fnv-12):

```
{{ crypto.FNV32a "Hello world" }} → 1498229191
```
