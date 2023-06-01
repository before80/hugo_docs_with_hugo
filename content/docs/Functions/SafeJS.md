+++
title = "safeJS"
weight = 101
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# safeJS

[https://gohugo.io/functions/safejs/](https://gohugo.io/functions/safejs/)

Declares the provided string as a known safe JavaScript string.

## 语法

```
safeJS INPUT
```

In this context, *safe* means the string encapsulates a known safe EcmaScript5 Expression (e.g., `(x + y * z())`).

Template authors are responsible for ensuring that typed expressions do not break the intended precedence and that there is no statement/expression ambiguity as when passing an expression like `{ foo:bar() }\n['foo']()`, which is both a valid expression and a valid program with a very different meaning.

Example: Given `hash = "619c16f"` defined in the front matter of your `.md` file:

- `<script>var form_{{ .Params.hash | safeJS }};…</script>` → `<script>var form_619c16f;…</script>`
- `<script>var form_{{ .Params.hash }};…</script>` → `<script>var form_"619c16f";…</script>`

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
