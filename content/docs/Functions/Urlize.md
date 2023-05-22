+++
title = "Urlize"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# urlize

[https://gohugo.io/functions/urlize/](https://gohugo.io/functions/urlize/)

Takes a string, sanitizes it for usage in URLs, and converts spaces to hyphens.

## 语法

```
urlize INPUT
```

The following examples pull from a content file with the following front matter:

xxxxxxxxxx2 1{{ upper "BatMan" }} → "BATMAN"2{{ "BatMan" | upper }} → "BATMAN"go-html-template

=== "yaml"

    ``` yaml
    ---
    location: Chicago IL
    tags:
    - pizza
    - beer
    - hot dogs
    title: The World's Greatest City
    ---
    ```

=== "toml"

    ``` toml
    +++
    location = 'Chicago IL'
    tags = ['pizza', 'beer', 'hot dogs']
    title = "The World's Greatest City"
    +++
    ```

=== "json"

    ``` json
    {
       "location": "Chicago IL",
       "tags": [
          "pizza",
          "beer",
          "hot dogs"
       ],
       "title": "The World's Greatest City"
    }
    ```

The following might be used as a partial within a [single page template](https://gohugo.io/templates/single-page-templates/):

layouts/partials/content-header.html

```go-html-template
<header>
    <h1>{{ .Title }}</h1>
    {{ with .Params.location }}
        <div><a href="/locations/{{ . | urlize }}">{{ . }}</a></div>
    {{ end }}
    <!-- Creates a list of tags for the content and links to each of their pages -->
    {{ with .Params.tags }}
    <ul>
        {{ range .}}
            <li>
                <a href="/tags/{{ . | urlize }}">{{ . }}</a>
            </li>
        {{ end }}
    </ul>
    {{ end }}
</header>
```

The preceding partial would then output to the rendered page as follows:

```html
<header>
  <h1>The World&#39;s Greatest City</h1>
  <div><a href="/locations/chicago-il">Chicago IL</a></div>
  <ul>
    <li>
      <a href="/tags/pizza">pizza</a>
    </li>
    <li>
      <a href="/tags/beer">beer</a>
    </li>
    <li>
      <a href="/tags/hot-dogs">hot dogs</a>
    </li>
  </ul>
</header>
```

## 另请参阅

- [safeURL](https://gohugo.io/functions/safeurl/)
- [Links and Cross References](https://gohugo.io/content-management/cross-references/)
- [URL Management](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
