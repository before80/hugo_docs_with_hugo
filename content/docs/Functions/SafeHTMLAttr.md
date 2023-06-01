+++
title = "SafeHTMLAttr"
weight = 100
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# safeHTMLAttr

[https://gohugo.io/functions/safehtmlattr/](https://gohugo.io/functions/safehtmlattr/)

Declares the provided string as a safe HTML attribute.

## 语法

```
safeHTMLAttr INPUT
```

Given a site configuration that contains this menu entry:

config.

=== "yaml"

    ``` yaml
    menu:
      main:
      - name: IRC
        url: irc://irc.freenode.net/#golang
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.main]]
      name = 'IRC'
      url = 'irc://irc.freenode.net/#golang'
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": [
             {
                "name": "IRC",
                "url": "irc://irc.freenode.net/#golang"
             }
          ]
       }
    }
    ```



Attempting to use the `url` value directly in an attribute:

```go-html-template
{{ range site.Menus.main }}
  <a href="{{ .URL }}">{{ .Name }}</a>
{{ end }}
```

Will produce:

```html
<a href="#ZgotmplZ">IRC</a>
```

`ZgotmplZ` is a special value, inserted by Go’s [template/html](https://pkg.go.dev/html/template) package, that indicates that unsafe content reached a CSS or URL context.

To override the safety check, use the `safeHTMLAttr` function:

```go-html-template
{{ range site.Menus.main }}
  <a {{ printf "href=%q" .URL | safeHTMLAttr }}>{{ .Name }}</a>
{{ end }}
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
