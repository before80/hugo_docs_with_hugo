+++
title = "safeURL"
weight = 102
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# safeURL

[https://gohugo.io/functions/safeurl/](https://gohugo.io/functions/safeurl/)

Declares the provided string as a safe URL or URL substring.

## 语法

```
safeURL INPUT
```

`safeURL` declares the provided string as a "safe" URL or URL substring (see [RFC 3986](https://tools.ietf.org/html/rfc3986)). A URL like `javascript:checkThatFormNotEditedBeforeLeavingPage()` from a trusted source should go in the page, but by default dynamic `javascript:` URLs are filtered out since they are a frequently exploited injection vector.

Without `safeURL`, only the URI schemes `http:`, `https:` and `mailto:` are considered safe by Go templates. If any other URI schemes (e.g., `irc:` and `javascript:`) are detected, the whole URL will be replaced with `#ZgotmplZ`. This is to "defang" any potential attack in the URL by rendering it useless.

The following examples use a [site `config.toml`](https://gohugo.io/getting-started/configuration/) with the following [menu entry](https://gohugo.io/content-management/menus/):

config.

=== "yaml"

    ``` yaml
    menu:
      main:
      - name: 'IRC: #golang at freenode'
        url: irc://irc.freenode.net/#golang
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.main]]
      name = 'IRC: #golang at freenode'
      url = 'irc://irc.freenode.net/#golang'
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": [
             {
                "name": "IRC: #golang at freenode",
                "url": "irc://irc.freenode.net/#golang"
             }
          ]
       }
    }
    ```

The following is an example of a sidebar partial that may be used in conjunction with the preceding front matter example:

layouts/partials/bad-url-sidebar-menu.html

```go-html-template
<!-- This unordered list may be part of a sidebar menu -->
<ul>
  {{ range .Site.Menus.main }}
    <li><a href="{{ .URL }}">{{ .Name }}</a></li>
  {{ end }}
</ul>
```

This partial would produce the following HTML output:

```html
<!-- This unordered list may be part of a sidebar menu -->
<ul>
  <li><a href="#ZgotmplZ">IRC: #golang at freenode</a></li>
</ul>
```

The odd output can be remedied by adding `| safeURL` to our `.URL` page variable:

layouts/partials/correct-url-sidebar-menu.html

```go-html-template
<!-- This unordered list may be part of a sidebar menu -->
<ul>
    <li><a href="{{ .URL | safeURL }}">{{ .Name }}</a></li>
</ul>
```

With the `.URL` page variable piped through `safeURL`, we get the desired output:

```html
<ul class="sidebar-menu">
  <li><a href="irc://irc.freenode.net/#golang">IRC: #golang at freenode</a></li>
</ul>
```

## 另请参阅

- [urlize](https://gohugo.io/functions/urlize/)
- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
