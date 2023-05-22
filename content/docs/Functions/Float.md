+++
title = "Float"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# float

[https://gohugo.io/functions/float/](https://gohugo.io/functions/float/)

Casts a value to a decimal (base 10) floating point value.

## 语法

```
float INPUT
```

With a decimal (base 10) input:

```go-html-template
{{ float 11 }} → 11 (float64)
{{ float "11" }} → 11 (float64)

{{ float 11.1 }} → 11.1 (float64)
{{ float "11.1" }} → 11.1 (float64)

{{ float 11.9 }} → 11.9 (float64)
{{ float "11.9" }} → 11.9 (float64)
```

With a binary (base 2) input:

```go-html-template
{{ float 0b11 }} → 3 (float64)
```

With an octal (base 8) input (use either notation):

```go-html-template
{{ float 011 }} → 9 (float64)
{{ float "011" }} → 11 (float64)

{{ float 0o11 }} → 9 (float64)
```

With a hexadecimal (base 16) input:

```go-html-template
{{ float 0x11 }} → 17 (float64)
```

## 另请参阅

- [int](https://gohugo.io/functions/int/)
- [string](https://gohugo.io/functions/string/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
