+++
title = "内容视图模板"
weight = 11
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Content View Templates - 内容视图模板

[https://gohugo.io/templates/views/](https://gohugo.io/templates/views/)

​	Hugo可以渲染内容的替代视图，这在列表和摘要视图中特别有用。 

​	这些替代的内容视图在[列表模板](https://gohugo.io/templates/lists/)中特别有用。

​	以下是内容视图的常见用例：

- 您希望在主页上显示每种类型的内容，但仅以有限的[摘要视图](https://gohugo.io/content-management/summaries/)显示。 
- 您只想在[分类列表页面](https://gohugo.io/templates/taxonomy-templates/)上显示您的内容的项目列表。视图通过将每种不同类型的内容的渲染委托给内容本身来使此过程变得非常简单。

## 创建内容视图 

​	要创建新视图，请在每个不同的内容类型目录中创建具有视图名称的模板。以下示例包含用于`posts`和`project`内容类型的"li"视图和"summary"视图。正如您所看到的，这些视图与[单个内容视图](https://gohugo.io/templates/single-page-templates/)模板`single.html`并排。您甚至可以为给定类型提供特定的视图，并继续使用`_default/single.html`作为主视图。

```txt
  ▾ layouts/
    ▾ posts/
        li.html
        single.html
        summary.html
    ▾ project/
        li.html
        single.html
        summary.html
```

​	Hugo还支持使用默认内容模板，以在没有为该类型提供特定内容视图模板的情况下使用。内容视图也可以在`_default`目录中定义，并且将像列表和单个模板一样工作，最终作为查找顺序的一部分向下传递到`_default`目录中。

```txt
▾ layouts/
  ▾ _default/
      li.html
      single.html
      summary.html
```

## 哪个模板将被渲染？ 

​	以下是[内容视图](https://gohugo.io/templates/lookup-order/)的查找顺序：

1. `/layouts/<TYPE>/<VIEW>.html`
2. `/layouts/_default/<VIEW>.html`
3. `/themes/<THEME>/layouts/<TYPE>/<VIEW>.html`
4. `/themes/<THEME>/layouts/_default/<VIEW>.html`

## 示例：列表中的内容视图 

​	以下示例演示了如何在[列表模板](https://gohugo.io/templates/lists/)中使用内容视图。

### `list.html` 

​	在此示例中，将`.Render`被传递到模板中以调用[`render`函数](https://gohugo.io/functions/render/)。 `.Render`是一种特殊的函数，它指示内容使用第一个参数提供的视图模板渲染自身。在本例中，该模板将渲染以下`summary.html`视图：

layouts/_default/list.html

```go-html-template
<main id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
      {{ .Render "summary" }}
    {{ end }}
  </div>
</main>
```

### `summary.html` 

​	Hugo将整个页面对象传递给以下`summary.html`视图模板。（有关完整列表，请参见[页面变量](https://gohugo.io/variables/page/)。）

layouts/_default/summary.html

```go-html-template
<article class="post">
  <header>
    <h2><a href='{{ .Permalink }}'> {{ .Title }}</a> </h2>
    <div class="post-meta">{{ .Date.Format "Mon, Jan 2, 2006" }} - {{ .FuzzyWordCount }} Words </div>
  </header>
  {{ .Summary }}
  <footer>
  <a href='{{ .Permalink }}'><nobr>Read more →</nobr></a>
  </footer>
</article>
```

### `li.html` 

​	继续上一个示例，我们可以通过更改调用 `.Render` 函数中的参数来使用较小的 `li.html` 视图（即 `{{ .Render "li" }}`）。

layouts/_default/li.html

```go-html-template
<li>
  <a href="{{ .Permalink }}">{{ .Title }}</a>
  <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
</li>
```

## 另请参阅

- [.Render](https://gohugo.io/functions/render/)
