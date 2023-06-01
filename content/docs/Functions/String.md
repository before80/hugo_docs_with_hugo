+++
title = "String"
weight = 112
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# string

[https://gohugo.io/functions/string/](https://gohugo.io/functions/string/)

Cast a value to a string.

## 语法

```
string INPUT
```

With a decimal (base 10) input:

```go-html-template
{{ string 11 }} → 11 (string)
{{ string "11" }} → 11 (string)

{{ string 11.1 }} → 11.1 (string)
{{ string "11.1" }} → 11.1 (string)

{{ string 11.9 }} → 11.9 (string)
{{ string "11.9" }} → 11.9 (string)
```

With a binary (base 2) input:

```go-html-template
{{ string 0b11 }} → 3 (string)
{{ string "0b11" }} → 0b11 (string)
```

With an octal (base 8) input (use either notation):

```go-html-template
{{ string 011 }} → 9 (string)
{{ string "011" }} → 011 (string)

{{ string 0o11 }} → 9 (string)
{{ string "0o11" }} → 0o11 (string)
```

With a hexadecimal (base 16) input:

```go-html-template
{{ string 0x11 }} → 17 (string)
{{ string "0x11" }} → 0x11 (string)
```

## 另请参阅

- [float](https://gohugo.io/functions/float/)
- [int](https://gohugo.io/functions/int/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
