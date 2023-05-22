+++
title = "Urlquery"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# urlquery

[https://gohugo.io/functions/urlquery/](https://gohugo.io/functions/urlquery/)

Returns the escaped value of the textual representation of its arguments in a form suitable for embedding in a URL query.

## 语法

```
urlquery INPUT [INPUT]...
```

This template code:

```go-html-template
{{ $u := urlquery "https://" "example.com" | safeURL }}
<a href="https://example.org?url={{ $u }}">Link</a>
```

Is rendered to:

```html
<a href="https://example.org?url=https%3A%2F%2Fexample.com">Link</a>
```

## 另请参阅

- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
- [querify](https://gohugo.io/functions/querify/)
