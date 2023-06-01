+++
title = "Group"
weight = 43
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# group

[https://gohugo.io/functions/group/](https://gohugo.io/functions/group/)

`group` groups a list of pages.

## 语法

```
PAGES | group KEY
```

layouts/partials/groups.html



```go-html-template
{{ $new := .Site.RegularPages | first 10 | group "New" }}
{{ $old := .Site.RegularPages | last 10 | group "Old" }}
{{ $groups := slice $new $old }}
{{ range $groups }}
<h3>{{ .Key }}{{/* Prints "New", "Old" */}}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```

The page group you get from `group` is of the same type you get from the built-in [group methods](https://gohugo.io/templates/lists#group-content) in Hugo. The above example can even be [paginated](https://gohugo.io/templates/pagination/#list-paginator-pages).

## 另请参阅

- [append](https://gohugo.io/functions/append/)
- [complement](https://gohugo.io/functions/complement/)
- [intersect](https://gohugo.io/functions/intersect/)
- [symdiff](https://gohugo.io/functions/symdiff/)
- [union](https://gohugo.io/functions/union/)
