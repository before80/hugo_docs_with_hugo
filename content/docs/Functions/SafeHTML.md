+++
title = "SafeHTML"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# safeHTML

[https://gohugo.io/functions/safehtml/](https://gohugo.io/functions/safehtml/)

Declares a provided string as a "safe" HTML document to avoid escaping by Go templates.

## 语法

```
safeHTML INPUT
```

It should not be used for HTML from a third-party, or HTML with unclosed tags or comments.

Given a site-wide [`config.toml`](https://gohugo.io/getting-started/configuration/) with the following `copyright` value:

config.

=== "yaml"

    ``` yaml
    copyright: © 2015 Jane Doe.  <a href="https://creativecommons.org/licenses/by/4.0/">Some
      rights reserved</a>.
    ```

=== "toml"

    ``` toml
    copyright = '© 2015 Jane Doe.  <a href="https://creativecommons.org/licenses/by/4.0/">Some rights reserved</a>.'
    ```

=== "json"

    ``` json
    {
       "copyright": "© 2015 Jane Doe.  \u003ca href=\"https://creativecommons.org/licenses/by/4.0/\"\u003eSome rights reserved\u003c/a\u003e."
    }
    ```



`{{ .Site.Copyright | safeHTML }}` in a template would then output:

```html
© 2015 Jane Doe.  <a href="https://creativecommons.org/licenses/by/4.0/">Some rights reserved</a>.
```

However, without the `safeHTML` function, html/template assumes `.Site.Copyright` to be unsafe and therefore escapes all HTML tags and renders the whole string as plain text:

```html
<p>© 2015 Jane Doe.  &lt;a href=&#34;https://creativecommons.org/licenses by/4.0/&#34;&gt;Some rights reserved&lt;/a&gt;.</p>
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
