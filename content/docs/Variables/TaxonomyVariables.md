+++
title = "分类法（Taxonomy）变量"
weight = 5
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Taxonomy Variables - 分类法（Taxonomy）变量

[https://gohugo.io/variables/taxonomy/](https://gohugo.io/variables/taxonomy/)

​	Hugo 的分类法系统向分类法和条目模板公开了变量。

## 分类模板 

​	由分类法模板渲染的页面的 `.Kind` 设置为 `taxonomy`，`.Type` 设置为分类法名称。

​	在分类法模板中，您可以访问 `.Site`、`.Page`、`.Section` 和 `.File` 变量，以及以下*分类法*变量：

### .Data.Singular

​	分类法的单数形式名称（例如， `tags => tag`）。

### .Data.Plural

​	分类法的复数形式名称（例如， `tags => tags`）。

### .Data.Pages

​	与此分类法相关的条目页面集合。别名为 `.Pages` 。

### .Data.Terms

​	一个与此分类法相关的条目和加权页面的映射。

### .Data.Terms.Alphabetical

​	一个与此分类法相关的条目和加权页面的映射，按字母顺序升序排序。使用 `.Data.Terms.Alphabetical.Reverse` 可以反转排序顺序。

### .Data.Terms.ByCount

​	一个与此分类法相关的条目和加权页面的映射，按计数升序排序。使用 `.Data.Terms.ByCount.Reverse` 可以反转排序顺序。

## Term templates 

​	由条目模板渲染的页面的 `.Kind` 设置为 `term`，`.Type` 设置为分类法名称。

In term templates you may access `.Site`, `.Page`. `.Section`, and `.File` variables, as well as the following *term* variables:

在分类项模板中，您可以访问 .Site、.Page、.Section 和 .File 变量，以及以下分类项变量：

​	在分类法条目模板中，您可以访问 `.Site`、`.Page`、`.Section` 和 `.File` 变量，以及以下*条目*变量：

### .Data.Singular

​	分类法的单数形式名称（例如 `tags => tag`）。

### .Data.Plural

​	分类法的复数形式名称（例如 `tags => tags`）。

### .Data.Pages

​	与此条目相关的内容页面集合。别名为 `.Pages` 。

### .Data.Term

​	条目本身（例如， `tag-one`）。

## 从任何模板访问分类法数据 

​	从任何模板中访问整个分类法数据结构，使用 `site.Taxonomies`。这将返回一个包含分类法、条目和与每个条目相关的加权内容页面集合的映射。例如：

```json
{
  "categories": {
    "news": [
      {
        "Weight": 0,
        "Page": {
          "Title": "Post 1",
          "Date": "2022-12-18T15:13:35-08:00"
          ...
          }
      },
      {
        "Weight": 0,
        "Page": {
          "Title": "Post 2",
          "Date": "2022-12-18T15:13:46-08:00",
          ...
        }
      }
    ]
  },
  "tags": {
    "international": [
      {
        "Weight": 0,
        "Page": {
          "Title": "Post 1",
          "Date": "2021-01-01T00:00:00Z"
          ... 
        }
      }
    ]
  }
}
```

Access a subset of the taxonomy data structure by chaining one or more identifiers, or by using the [`index`](https://gohugo.io/functions/index-function/) function with one or more keys. For example, to access the collection of weighted content pages related to the news category, use either of the following:

​	通过链接一个或多个标识符，或使用 [`index`](https://gohugo.io/functions/index-function/) 函数加上一个或多个键，可以访问分类法数据结构的子集。例如，要访问与新闻类别相关的加权内容页面集合，请使用以下任一方法：

```go-html-template
{{ $pages := site.Taxonomies.categories.news }}
{{ $pages := index site.Taxonomies "categories" "news" }}
```

​	例如，将整个分类法数据结构渲染为嵌套的无序列表：

```go-html-template
<ul>
  {{ range $taxonomy, $terms := site.Taxonomies }}
    <li>
      {{ with site.GetPage $taxonomy }}
        <a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a>
      {{ end }}
      <ul>
        {{ range $term, $weightedPages := $terms }}
        <li>
          {{ with site.GetPage (path.Join $taxonomy $term) }}
            <a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a>
          {{ end }}
        </li>
          <ul>
            {{ range $weightedPages }}
              <li>
                <a href="{{ .RelPermalink }}"> {{ .LinkTitle }}</a>
              </li>
            {{ end }}
          </ul>
        {{ end }}
      </ul>
    </li>
  {{ end }}
</ul>
```

​	有关更多示例，请参见[分类法模板](https://gohugo.io/templates/taxonomy-templates/)。
