+++
title = "单页模板"
weight = 10
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Single Page Templates - 单页模板 

​	在 Hugo 中，内容的主要视图是单个视图。Hugo 会为每个 Markdown 文件提供相应的单个模板进行渲染。

## 单页模板查找顺序 

​	请参阅[模板查找](https://gohugo.io/templates/lookup-order/)。

## 单页模板示例 

​	内容页面的类型是 `page`，因此可以在它们的模板中使用所有 [页面变量](https://gohugo.io/variables/page/) 和 [站点变量](https://gohugo.io/variables/site/)。

### `posts/single.html` 

​	这个单页模板使用了 Hugo 的 [基础模板](https://gohugo.io/templates/base/)、[`.Format` 函数](https://gohugo.io/functions/format/) 来处理日期、[`.WordCount` 页面变量](https://gohugo.io/variables/page/) 以及遍历单一内容的特定[分类法](https://gohugo.io/templates/taxonomy-templates/#display-a-single-piece-of-contents-taxonomies)。[`with`](https://gohugo.io/functions/with/) 也用来检查是否在前置元数据中设置了分类法。

layouts/posts/single.html

```go-html-template
{{ define "main" }}

<section id="main">
  <h1 id="title">{{ .Title }}</h1>
  <div>
    <article id="content">
      {{ .Content }}
    </article>
  </div>
</section>
<aside id="meta">
  <div>
  <section>
    <h4 id="date"> {{ .Date.Format "Mon Jan 2, 2006" }} </h4>
    <h5 id="wordcount"> {{ .WordCount }} Words </h5>
  </section>
    {{ with .GetTerms "topics" }}
      <ul id="topics">
        {{ range . }}
          <li><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></li>
        {{ end }}
      </ul>
    {{ end }}
    {{ with .GetTerms "tags" }}
      <ul id="tags">
        {{ range . }}
          <li><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></li>
        {{ end }}
      </ul>
    {{ end }}
  </div>
  <div>
    {{ with .PrevInSection }}
      <a class="previous" href="{{ .Permalink }}"> {{ .Title }}</a>
    {{ end }}
    {{ with .NextInSection }}
      <a class="next" href="{{ .Permalink }}"> {{ .Title }}</a>
    {{ end }}
  </div>
</aside>
{{ end }}
```

​	要轻松生成一个内容类型的新实例（例如，在像 `project/` 这样的章节中生成新的 `.md` 文件），并预先配置好前置元数据，请使用[内容原型](https://gohugo.io/content-management/archetypes/)。

## 另请参阅

- [创建自己的简码 ](https://gohugo.io/templates/shortcode-templates/)
- [Hugo 的查找顺序 ](https://gohugo.io/templates/lookup-order/)
- [页面 Bundles](https://gohugo.io/content-management/page-bundles/)
- [RSS 模板 ](https://gohugo.io/templates/rss/)
- [章节页面模板](https://gohugo.io/templates/section-templates/)
