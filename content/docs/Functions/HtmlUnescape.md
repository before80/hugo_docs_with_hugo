+++
title = "htmlUnescape"
weight = 48
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# htmlUnescape

[https://gohugo.io/functions/htmlunescape/](https://gohugo.io/functions/htmlunescape/)

Returns the given string with HTML escape codes un-escaped.

## 语法

```
htmlUnescape INPUT
```

`htmlUnescape` returns the given string with HTML escape codes un-escaped.

Remember to pass the output of this to `safeHTML` if fully un-escaped characters are desired. Otherwise, the output will be escaped again as normal.

```go-html-template
{{ htmlUnescape "Hugo &amp; Caddy &gt; WordPress &amp; Apache" }} → "Hugo & Caddy > WordPress & Apache"
```
