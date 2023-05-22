+++
title = "Jsonify"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# jsonify

[https://gohugo.io/functions/jsonify/](https://gohugo.io/functions/jsonify/)

Encodes a given object to JSON.

## 语法

```
jsonify INPUT
jsonify OPTIONS INPUT
```

Jsonify encodes a given object to JSON.

To customize the printing of the JSON, pass a dictionary of options as the first argument. Supported options are "prefix" and "indent". Each JSON element in the output will begin on a new line beginning with *prefix* followed by one or more copies of *indent* according to the indentation nesting.

```go-html-template
{{ dict "title" .Title "content" .Plain | jsonify }}
{{ dict "title" .Title "content" .Plain | jsonify (dict "indent" "  ") }}
{{ dict "title" .Title "content" .Plain | jsonify (dict "prefix" " " "indent" "  ") }}
```

## Jsonify options 

- indent ("")

  Indentation to use.

- prefix ("")

  Indentation prefix.

- noHTMLEscape (false)

  Disable escaping of problematic HTML characters inside JSON quoted strings. The default behavior is to escape &, <, and > to \u0026, \u003c, and \u003e to avoid certain safety problems that can arise when embedding JSON in HTML.

See also the `.PlainWords`, `.Plain`, and `.RawContent` [page variables](https://gohugo.io/variables/page/).

## 另请参阅

- [Configure Hugo](https://gohugo.io/getting-started/configuration/)
- [Data Templates](https://gohugo.io/templates/data-templates/)
- [Front Matter](https://gohugo.io/content-management/front-matter/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
