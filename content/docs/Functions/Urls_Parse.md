+++
title = "urls.Parse"
weight = 140
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# urls.Parse

[https://gohugo.io/functions/urls.parse/](https://gohugo.io/functions/urls.parse/)

Parses a URL into a URL structure.

## 语法

```
urls.Parse URL
```

The `urls.Parse` function parses a URL into a [URL structure](https://godoc.org/net/url#URL). The URL may be relative (a path, without a host) or absolute (starting with a [scheme](https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml#uri-schemes-1)). Hugo throws an error when parsing an invalid URL.

```go-html-template
{{ $url := "https://example.org:123/foo?a=6&b=7#bar" }}
{{ $u := urls.Parse $url }}

{{ $u.IsAbs }} → true
{{ $u.Scheme }} → https
{{ $u.Host }} → example.org:123
{{ $u.Hostname }} → example.org
{{ $u.RequestURI }} → /foo?a=6&b=7
{{ $u.Path }} → /foo
{{ $u.Query }} → map[a:[6] b:[7]]
{{ $u.Query.a }} → [6]
{{ $u.Query.Get "a" }} → 6
{{ $u.Query.Has "b" }} → true
{{ $u.Fragment }} → bar
```

## 另请参阅

- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
- [querify](https://gohugo.io/functions/querify/)
