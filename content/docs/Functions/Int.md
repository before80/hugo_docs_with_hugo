+++
title = "Int"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# int

[https://gohugo.io/functions/int/](https://gohugo.io/functions/int/)

Casts a value to a decimal (base 10) integer.

## 语法

```
int INPUT
```

With a decimal (base 10) input:

```go-html-template
{{ int 11 }} → 11 (int)
{{ int "11" }} → 11 (int)

{{ int 11.1 }} → 11 (int)
{{ int 11.9 }} → 11 (int)
```

With a binary (base 2) input:

```go-html-template
{{ int 0b11 }} → 3 (int)
{{ int "0b11" }} → 3 (int)
```

With an octal (base 8) input (use either notation):

```go-html-template
{{ int 011 }} → 9 (int)
{{ int "011" }} → 9 (int)

{{ int 0o11 }} → 9 (int)
{{ int "0o11" }} → 9 (int)
```

With a hexadecimal (base 16) input:

```go-html-template
{{ int 0x11 }} → 17 (int)
{{ int "0x11" }} → 17 (int)
```

Values with a leading zero are octal (base 8). When casting a string representation of a decimal (base 10) number, remove leading zeros:

```
{{ strings.TrimLeft "0" "0011" | int }} → 11
```

## 另请参阅

- [float](https://gohugo.io/functions/float/)
- [string](https://gohugo.io/functions/string/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
