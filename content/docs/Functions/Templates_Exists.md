+++
title = "Templates_Exists"
weight = 127
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# templates.Exists

[https://gohugo.io/functions/templates.exists/](https://gohugo.io/functions/templates.exists/)

Checks whether a template file exists under the given path relative to the `layouts` directory.

## 语法

```
templates.Exists PATH
```

A template file is any file living below the `layouts` directories of either the project or any of its theme components including partials and shortcodes.

The function is particularly handy with dynamic path. The following example ensures the build will not break on a `.Type` missing its dedicated `header` partial.

```go-html-template
{{ $partialPath := printf "headers/%s.html" .Type }}
{{ if templates.Exists ( printf "partials/%s" $partialPath ) }}
  {{ partial $partialPath . }}
{{ else }}
  {{ partial "headers/default.html" . }}
{{ end }}
```

## 另请参阅

- [Create Your Own Shortcodes](https://gohugo.io/templates/shortcode-templates/)
- [Hugo's Lookup Order](https://gohugo.io/templates/lookup-order/)
- [RSS Templates](https://gohugo.io/templates/rss/)
- [Section Page Templates](https://gohugo.io/templates/section-templates/)
- [Single Page Templates](https://gohugo.io/templates/single-page-templates/)
