+++
title = "AbsURL"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# absURL

[https://gohugo.io/functions/absurl/](https://gohugo.io/functions/absurl/)

Returns an absolute URL.

## 语法

```
absURL INPUT
```

With multilingual configurations, use the [`absLangURL`](https://gohugo.io/functions/abslangurl/) function instead. The URL returned by this function depends on:

- Whether the input begins with a slash
- The `baseURL` in site configuration

### Input does not begin with a slash 

If the input does not begin with a slash, the resulting URL will be correct regardless of the `baseURL`.

With `baseURL = https://example.org/`

```go-html-template
{{ absURL "" }}           →   https://example.org/
{{ absURL "articles" }}   →   https://example.org/articles
{{ absURL "style.css" }}  →   https://example.org/style.css
```

With `baseURL = https://example.org/docs/`

```go-html-template
{{ absURL "" }}           →   https://example.org/docs/
{{ absURL "articles" }}   →   https://example.org/docs/articles
{{ absURL "style.css" }}  →   https://example.org/docs/style.css
```

### Input begins with a slash 

If the input begins with a slash, the resulting URL will be incorrect when the `baseURL` includes a subdirectory. With a leading slash, the function returns a URL relative to the protocol+host section of the `baseURL`.

With `baseURL = https://example.org/`

```go-html-template
{{ absURL "/" }}          →   https://example.org/
{{ absURL "/articles" }}  →   https://example.org/articles
{{ absURL "/style.css" }} →   https://example.org/style.css
```

With `baseURL = https://example.org/docs/`

```go-html-template
{{ absURL "/" }}          →   https://example.org/
{{ absURL "/articles" }}  →   https://example.org/articles
{{ absURL "/style.css" }} →   https://example.org/style.css
```

The last three examples are not desirable in most situations. As a best practice, never include a leading slash when using this function.

## 另请参阅

- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [relLangURL](https://gohugo.io/functions/rellangurl/)
- [relURL](https://gohugo.io/functions/relurl/)
- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
