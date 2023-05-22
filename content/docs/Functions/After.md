+++
title = "After"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# after

[https://gohugo.io/functions/after/](https://gohugo.io/functions/after/)

`after` slices an array to only the items after the Nth item.

## 语法

```
after INDEX COLLECTION
```

The following shows `after` being used in conjunction with the [`slice` function](https://gohugo.io/functions/slice/):

```go-html-template
{{ $data := slice "one" "two" "three" "four" }}
{{ range after 2 $data }}
    {{ . }}
{{ end }}
→ ["three", "four"]
```

## Example of `after` with `first`: 2nd–4th Most Recent Articles 

You can use `after` in combination with the [`first` function](https://gohugo.io/functions/first/) and Hugo’s [powerful sorting methods](https://gohugo.io/templates/lists/#order-content). Let’s assume you have a list page at `example.com/articles`. You have 10 articles, but you want your templating for the [list/section page](https://gohugo.io/templates/section-templates/) to show only two rows:

1. The top row is titled "Featured" and shows only the most recently published article (i.e. by `publishdate` in the content files’ front matter).
2. The second row is titled "Recent Articles" and shows only the 2nd- to 4th-most recently published articles.

layouts/section/articles.html



```go-html-template
{{ define "main" }}
<section class="row featured-article">
  <h2>Featured Article</h2>
  {{ range first 1 .Pages.ByPublishDate.Reverse }}
  <header>
      <h3><a href="{{ . Permalink }}">{{ .Title }}</a></h3>
  </header>
  <p>{{ .Description }}</p>
{{ end }}
</section>
<div class="row recent-articles">
  <h2>Recent Articles</h2>
  {{ range first 3 (after 1 .Pages.ByPublishDate.Reverse) }}
    <section class="recent-article">
      <header>
          <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
      </header>
      <p>{{ .Description }}</p>
    </section>
  {{ end }}
</div>
{{ end }}
```

## 另请参阅

- [.Scratch](https://gohugo.io/functions/scratch/)
- [delimit](https://gohugo.io/functions/delimit/)
- [first](https://gohugo.io/functions/first/)
- [range](https://gohugo.io/functions/range/)
