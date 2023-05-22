+++
title = "分类法（Taxonomy）模板 "
weight = 9
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Taxonomy Templates - 分类法（Taxonomy）模板 

[https://gohugo.io/templates/taxonomy-templates/](https://gohugo.io/templates/taxonomy-templates/)

​	Taxonomy（分类法）模板包括分类法列表页面、分类法条目页面以及在单页模板中使用分类法。

​	Hugo 支持用户定义的内容分组，称为**分类法**。分类法是展示内容之间逻辑关系的分类法方法。如果您对 Hugo 如何利用这个强大功能不熟悉，请参见[内容管理下的分类法](https://gohugo.io/content-management/taxonomies)。

​	Hugo 提供了多种在项目模板中使用分类法的方式： 

- 按照与分类法条目相关联的内容的方式在[分类法列表模板](https://gohugo.io/templates/taxonomy-templates/#taxonomy-list-templates)中显示。
- 以特定的顺序显示与分类法条目相关联的内容，具体方法是在[分类法列表模板](https://gohugo.io/templates/taxonomy-templates/#taxonomy-list-templates)中设置排序方式。
- 按照分类法的方式在[分类法条目模板](https://gohugo.io/templates/taxonomy-templates/#taxonomy-terms-templates)中显示。
- 在[单页模板](https://gohugo.io/templates/single-page-templates/)中列出单个内容的分类法条目。

## 分类法列表模板 

​	分类法列表页面模板是列表，因此具有可用于[列表页面](https://gohugo.io/templates/lists/)的所有变量和方法。

### 分类法列表模板查找顺序 

​	请参见[模板查找](https://gohugo.io/templates/lookup-order/)。

## 分类法条目模板 

### 分类法条目模板查找顺序 

​	请参见[模板查找](https://gohugo.io/templates/lookup-order/)。

### 分类法方法 

A Taxonomy is a `map[string]WeightedPages`.

​	分类法是一个 `map[string]WeightedPages`。

- .Get(term)

  返回条目的 WeightedPages。 

- .Count(term)

  分配给该条目的内容数量。

- .Alphabetical

  Returns an OrderedTaxonomy (slice) ordered by Term.

  返回一个按条目排序的 OrderedTaxonomy（切片）。 

- .ByCount

  返回一个按条目数量排序的 OrderedTaxonomy（切片）。

- .Reverse

  返回一个按相反顺序排序的 OrderedTaxonomy（切片）。必须与 一个OrderedTaxonomy 一起使用。 
  
  

### OrderedTaxonomy 

​	由于 Map 是无序的，因此 OrderedTaxonomy 是一个具有定义顺序的特殊结构。

```go
[]struct {
    Name          string
    WeightedPages WeightedPages
}
```

​	该切片的每个元素都有：

- .Term

  使用的条目。 

- .WeightedPages

  一个加权页面的切片。 

- .Count

  分配给该条目的内容数量。 

- .Pages

  分配给该条目的所有页面。所有[列表方法](https://gohugo.io/templates/lists/)都可用于此。

## WeightedPages 

​	WeightedPages是WeightedPage的一个切片。

```go
type WeightedPages []WeightedPage
```

- .Count(term)

  被分配到此条目的内容数量。

- .Pages

  返回一个页面的切片，可以使用任何 [列表方法](https://gohugo.io/templates/lists/) 进行排序。

## 在分类法条目模板中显示自定义元数据 

​	如果您需要为每个分类法条目显示自定义元数据，您需要在`/content/<TAXONOMY>/<TERM>/_index.md`路径下为该条目创建一个页面，并在其前置元数据中添加元数据，[如分类法文档中所述](https://gohugo.io/content-management/taxonomies/#add-custom-metadata-to-a-taxonomy-or-term)。以其中显示的演员分类法为例，在您的分类法条目模板中，您可以通过迭代变量`.Pages`来访问您的自定义字段：

```go-html-template
<ul>
    {{ range .Pages }}
        <li>
            <a href="{{ .Permalink }}">{{ .Title }}</a>
            {{ .Params.wikipedia }}
        </li>
    {{ end }}
</ul>
```

## 排序分类法 

​	分类法可以按字母键或分配给该键的内容数量排序。

### 按字母顺序示例

```go-html-template
<ul>
    {{ range .Data.Terms.Alphabetical }}
            <li><a href="{{ .Page.Permalink }}">{{ .Page.Title }}</a> {{ .Count }}</li>
    {{ end }}
</ul>
```

## 在分类法中排序内容 

​	Hugo在分类法中使用`date`和`weight`来排序内容。

​	在 Hugo 中，每篇内容可以选择性地被分配一个日期。它也可以为每个所属分类法分配一个权重。

​	当在分类法中迭代内容时，默认排序方式与用于章节和列表页面相同：首先按权重，然后按日期排序。这意味着，如果两篇内容的权重相同，则最近日期的内容将首先显示。

​	任何一篇内容的默认权重为0。零意味着"does not have a weight"，而不是"has a weight of numerical value zero"。

​	因此，权重为零的条目被特殊处理：如果两个页面的权重不相等，并且其中一个是零，则具有零权重的页面将始终出现在另一个页面之后，而不用考虑另一个页面的权重。因此，应谨慎使用零权重：例如，如果正权重和负权重都用于在两个方向上扩展序列，则具有零权重的页面将不会出现在列表的中间，而是在末尾。

### 分配权重 

​	每个内容可以分别为它所属的每个分类法（taxonomies）赋予一个权重（weight）。

content/example.md

=== "yaml"

    ``` yaml
    ---
    categories:
    - d
    categories_weight: 44
    tags:
    - a
    - b
    - c
    tags_weight: 22
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    categories = ['d']
    categories_weight = 44
    tags = ['a', 'b', 'c']
    tags_weight = 22
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "categories": [
          "d"
       ],
       "categories_weight": 44,
       "tags": [
          "a",
          "b",
          "c"
       ],
       "tags_weight": 22,
       "title": "Example"
    }
    ```



​	惯例是使用`taxonomyname_weight`。

​	在上面的例子中，这篇内容在渲染分配给"tag" 分类法中的"a"、"b" 和 "c" 值的页面时具有22的权重。

​	在渲染'd'类别时，它还被赋予了44的权重。

​	这样做可以使同一篇内容在不同的分类法中出现在不同的位置。

​	目前，分类法仅支持默认的内容排序方式，即权重->日期。

​	使用分类法将需要提供两种不同的模板。

​	这两中模板在模板章节中都有详细介绍。

​	[列表模板](https://gohugo.io/templates/lists/)是用于在单个HTML页面中渲染多篇内容的任一模板。此模板将用于生成所有自动创建的分类法页面。

​	[分类法模板](https://gohugo.io/templates/taxonomy-templates/)是用于生成给定模板的条目列表的模板。

​	除了使用 Hugo 自动生成的 [列表模板](https://gohugo.io/templates/lists/) 来创建分类法页面外，还有四种常见的方式可以展示您的分类法数据： 

1. 对于给定篇的内容，您可以列出附加的条目
3. 对于给定篇的内容，您可以列出具有相同条目的其他内容
5. 您可以列出某一分类法的所有条目
7. 您可以列出所有分类法（及其条目）

## 显示单篇内容的分类法

​	在内容模板中，您可能希望显示分配给该内容的分类法。

​	由于我们利用前置元数据系统为内容定义分类法，因此分配给每篇内容的分类法位于通常的位置（即 `.Params.<TAXONOMYPLURAL>`）。

### 示例：在单页模板中列出标签

```go-html-template
<ul>
    {{ range (.GetTerms "tags") }}
        <li><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></li>
    {{ end }}
</ul>
```

​	如果您想要内联列出分类法，您将需要注意标题中的可选复数结尾（如果有多个分类法），以及逗号。假设我们有一个名为 "directors" 的分类法，如 TOML 格式的前置元数据所示：`directors: [ "Joel Coen", "Ethan Coen" ]`。

​	要列出这样的分类法，请使用以下方法：

### 示例：在单页模板中使用逗号分隔标签

```go-html-template
{{ $taxo := "directors" }} <!-- Use the plural form here -->
{{ with .Param $taxo }}
    <strong>Director{{ if gt (len .) 1 }}s{{ end }}:</strong>
    {{ range $index, $director := . }}
        {{- if gt $index 0 }}, {{ end -}}
        {{ with $.Site.GetPage (printf "/%s/%s" $taxo $director) -}}
            <a href="{{ .Permalink }}">{{ $director }}</a>
        {{- end -}}
    {{- end -}}
{{ end }}
```

​	或者，如果只需要使用分隔符列出分类法，则可以使用[delimit 模板函数](https://gohugo.io/functions/delimit/)作为快捷方式。详见GitHub上的[#2143](https://github.com/gohugoio/hugo/issues/2143)讨论。

## 列出具有相同分类法条目的内容 

​	如果您正在使用分类法来管理一系列文章，您可以列出与同一分类法相关联的各个页面。这也是一种快速粗略的方法来展示相关内容：

```

```

### 示例：显示同一系列的内容

```go-html-template
<ul>
    {{ range .Site.Taxonomies.series.golang }}
        <li><a href="{{ .Page.RelPermalink }}">{{ .Page.Title }}</a></li>
    {{ end }}
</ul>
```

## 列出给定分类法中的所有内容 

​	这在侧边栏中作为"特色内容"将非常有用。您甚至可以通过为内容分配不同的条目来创建不同的"特色内容" 章节。

### 示例：对"Featured"内容进行分组

```go-html-template
<section id="menu">
    <ul>
        {{ range $key, $taxonomy := .Site.Taxonomies.featured }}
        <li>{{ $key }}</li>
        <ul>
            {{ range $taxonomy.Pages }}
            <li hugo-nav="{{ .RelPermalink }}"><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></li>
            {{ end }}
        </ul>
        {{ end }}
    </ul>
</section>
```

## 渲染站点的分类法 

​	如果您希望显示站点分类法的所有键列表，可以从每个页面都可以访问的[`.Site`变量](https://gohugo.io/variables/site/)中检索它们。

​	这可以采用标签云、菜单或简单列表的形式。

​	以下示例显示站点标签分类法中的所有条目：

### 示例：列出所有站点标签

```go-html-template
<ul>
    {{ range .Site.Taxonomies.tags }}
            <li><a href="{{ .Page.Permalink }}">{{ .Page.Title }}</a> {{ .Count }}</li>
    {{ end }}
</ul>
```

### 示例：列出所有分类法、条目和分配的内容 

​	这个示例将列出所有分类法及其条目，以及分配给每个条目的所有内容。

layouts/partials/all-taxonomies.html

```go-html-template
<section>
    <ul id="all-taxonomies">
        {{ range $taxonomy_term, $taxonomy := .Site.Taxonomies }}
            {{ with $.Site.GetPage (printf "/%s" $taxonomy_term) }}
                <li><a href="{{ .Permalink }}">{{ $taxonomy_term }}</a>
                    <ul>
                        {{ range $key, $value := $taxonomy }}
                            <li>{{ $key }}</li>
                            <ul>
                                {{ range $value.Pages }}
                                    <li hugo-nav="{{ .RelPermalink }}">
                                        <a href="{{ .Permalink }}">{{ .LinkTitle }}</a>
                                    </li>
                                {{ end }}
                            </ul>
                        {{ end }}
                    </ul>
                </li>
            {{ end }}
        {{ end }}
    </ul>
</section>
```

## `.Site.GetPage` 用于分类法 

​	由于分类法是列表，可以使用[`.GetPage`函数](https://gohugo.io/functions/getpage/)使用简洁的语法获取与特定分类法条目相关联的所有页面。下面对站点上所有标签进行全面的遍历，并链接到每个条目的单独分类页面，而不必使用[上面的"列出所有站点标签"示例](ttps://gohugo.io/templates/taxonomy-templates/#example-list-all-site-tags)中更脆弱的URL构建方法：

links-to-all-tags.html

```go-html-template
{{ $taxo := "tags" }}
<ul class="{{ $taxo }}">
    {{ with ($.Site.GetPage (printf "/%s" $taxo)) }}
        {{ range .Pages }}
            <li><a href="{{ .Permalink }}">{{ .Title }}</a></li>
        {{ end }}
    {{ end }}
</ul>
```

## 另请参阅

- [分类法 ](https://gohugo.io/content-management/taxonomies/)
- [原型 ](https://gohugo.io/content-management/archetypes/)
- [前置元数据](https://gohugo.io/content-management/front-matter/)
- [Hugo 中的内容列表 ](https://gohugo.io/templates/lists/)
- [.Param](https://gohugo.io/functions/param/)
