+++
title = "Querify"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# querify

[https://gohugo.io/functions/querify/](https://gohugo.io/functions/querify/)

Takes a set or slice of key-value pairs and returns a query string to be appended to URLs.

## 语法

```
querify KEY VALUE [KEY VALUE]...
querify COLLECTION
```

`querify` takes a set or slice of key-value pairs and returns a [query string](https://en.wikipedia.org/wiki/Query_string) that can be appended to a URL.

The following examples create a link to a search results page on Google.

```go-html-template
<a href="https://www.google.com?{{ (querify "q" "test" "page" 3) | safeURL }}">Search</a>

{{ $qs := slice "q" "test" "page" 3 }}
<a href="https://www.google.com?{{ (querify $qs) | safeURL }}">Search</a>
```

Both of these examples render the following HTML:

```html
<a href="https://www.google.com?page=3&q=test">Search</a>
```

## 另请参阅

- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
- [relLangURL](https://gohugo.io/functions/rellangurl/)
