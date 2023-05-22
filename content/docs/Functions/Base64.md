+++
title = "Base64"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# base64

[https://gohugo.io/functions/base64/](https://gohugo.io/functions/base64/)

`base64Encode` and `base64Decode` let you easily decode content with a base64 encoding and vice versa through pipes.

## 语法

```
base64Decode INPUT
base64Encode INPUT
{{ "Hugo" | base64Encode }} → "SHVnbw=="
{{ "SHVnbw==" | base64Decode }} → "Hugo"
```

## `base64` with APIs 

Using base64 to decode and encode becomes really powerful if we have to handle responses from APIs.

```go-html-template
{{ $resp := getJSON "https://api.github.com/repos/gohugoio/hugo/readme" }}
{{ $resp.content | base64Decode | markdownify }}
```

The response of the GitHub API contains the base64-encoded version of the [README.md](https://github.com/gohugoio/hugo/blob/master/README.md) in the Hugo repository. Now we can decode it and parse the Markdown. The final output will look similar to the rendered version on GitHub.
