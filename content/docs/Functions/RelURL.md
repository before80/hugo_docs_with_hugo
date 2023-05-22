+++
title = "RelURL"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# relURL

[https://gohugo.io/functions/relurl/](https://gohugo.io/functions/relurl/)

Returns a relative URL.

## 语法

```
relURL INPUT
```

With multilingual configurations, use the [`relLangURL`](https://gohugo.io/functions/rellangurl/) function instead. The URL returned by this function depends on:

- Whether the input begins with a slash
- The `baseURL` in site configuration

### Input does not begin with a slash 

If the input does not begin with a slash, the resulting URL will be correct regardless of the `baseURL`.

With `baseURL = https://example.org/`

```go-html-template
{{ relURL "" }}           →   /
{{ relURL "articles" }}   →   /articles
{{ relURL "style.css" }}  →   /style.css
```

With `baseURL = https://example.org/docs/`

```go-html-template
{{ relURL "" }}           →   /docs/
{{ relURL "articles" }}   →   /docs/articles
{{ relURL "style.css" }}  →   /docs/style.css
```

### Input begins with a slash 

If the input begins with a slash, the resulting URL will be incorrect when the `baseURL` includes a subdirectory. With a leading slash, the function returns a URL relative to the protocol+host section of the `baseURL`.

With `baseURL = https://example.org/`

```go-html-template
{{ relURL "/" }}          →   /
{{ relURL "/articles" }}  →   /articles
{{ relURL "style.css" }}  →   /style.css
```

With `baseURL = https://example.org/docs/`

```go-html-template
{{ relURL "/" }}          →   /
{{ relURL "/articles" }}  →   /articles
{{ relURL "/style.css" }} →   /style.css
```

The last three examples are not desirable in most situations. As a best practice, never include a leading slash when using this function.

## 另请参阅

- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
- [relLangURL](https://gohugo.io/functions/rellangurl/)
- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
