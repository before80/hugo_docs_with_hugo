+++
title = "在Hugo中的内容列表"
weight = 6
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Lists of Content in Hugo - 在Hugo中的内容列表 

https://gohugo.io/templates/lists/

​	列表在 Hugo 中在渲染站点主页、章节页面、分类列表或分类术语列表时具有特定的含义和用法。

## 什么是列表页面模板？

<iframe src="https://www.youtube.com/embed/8b2YTSMdMps" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

​	列表页面模板是用于在单个 HTML 页面中渲染多个内容的模板。唯一的例外是主页，它仍然是一个列表，但有自己的[专用模板](https://gohugo.io/templates/homepage/)。

​	Hugo 在其最真实的意义上使用列表这个术语；即按字母或数字顺序的一系列材料。Hugo 在任何传统上列出内容的输出 HTML 页面上都使用列表模板：

- [分类术语页面](https://gohugo.io/templates/taxonomy-templates/#taxonomy-terms-templates)
- [分类列表页面](https://gohugo.io/templates/taxonomy-templates/#taxonomy-list-templates)
- [章节列表页面](https://gohugo.io/templates/section-templates/)
- [RSS](https://gohugo.io/templates/rss/)

​	有关模板查找顺序，请参见[模板查找](https://gohugo.io/templates/lookup-order/)。

​	列表页面的概念源于[Web的分层心理模型](https://webstyleguide.com/wsg3/3-information-architecture/3-site-structure.html)，最好通过可视化进行演示：

![Image demonstrating a hierarchical website sitemap.](ListTemplates_img/site-hierarchy.svg)

## 列表默认值 

### 默认模板 

​	由于章节列表和分类列表（注意，不是[分类术语列表](https://gohugo.io/templates/taxonomy-templates/#taxonomy-terms-templates)）在模板方面都是列表，因此它们在查找顺序中都有相同的终止默认值 `_default/list.html` 或 `themes/<THEME>/layouts/_default/list.html`。此外，[章节列表](https://gohugo.io/templates/section-templates/)和[分类列表](https://gohugo.io/templates/taxonomy-templates/#taxonomy-list-templates)在 `_default` 中都有自己的默认列表模板。

​	有关完整参考，请参阅[模板查找顺序](https://gohugo.io/templates/lookup-order/)。

## 将内容和前置元数据添加到列表页

​	自从 v0.18 以来，[Hugo 中的所有内容都是`Page`](https://bepsays.com/en/2016/12/19/hugo-018/)。这意味着列表页面和主页可以有关联的内容文件（即`_index.md`），其中包含页面元数据（即前置元数据）和内容。

​	这种新模型允许您通过 `.Params` 包含特定于列表的前置元数据，并且意味着列表模板（例如 `layouts/_default/list.html`）可以访问所有[页面变量](https://gohugo.io/variables/page/)。

> ​	重要的是要注意，所有 `_index.md` 内容文件都将根据列表模板而不是[单个页面模板](https://gohugo.io/templates/single-page-templates/)进行渲染。



### 示例项目目录 

​	以下是一个典型的Hugo项目的content目录的示例：

```txt
.
...
├── content
|   ├── posts
|   |   ├── _index.md
|   |   ├── post-01.md
|   |   └── post-02.md
|   └── quote
|   |   ├── quote-01.md
|   |   └── quote-02.md
...
```

​	使用上述示例，假设您在`content/posts/_index.md`中有以下内容：

content/posts/_index.md

```md
---
title: My Go Journey
date: 2017-03-23
publishdate: 2017-03-24
---

I decided to start learning Go in March 2017.

Follow my journey through this new blog.
```

​	现在，您可以在列表模板中访问此`_index.md`的内容：

layouts/_default/list.html

```go-html-template
{{ define "main" }}
<main>
  <article>
    <header>
      <h1>{{ .Title} }</h1>
    </header>
    <!-- "{{ .Content} }" pulls from the markdown content of the corresponding _index.md -->
    {{ .Content }}
  </article>
  <ul>
    <!-- Ranges through content/posts/*.md -->
    {{ range .Pages }}
      <li>
        <a href="{{ .Permalink }}">{{ .Date.Format "2006-01-02" }} | {{ .Title }}</a>
      </li>
    {{ end }}
  </ul>
</main>
{{ end }}
```

​	上面将输出以下 HTML：

example.com/posts/index.html

```go-html-template
<!--top of your baseof code-->
<main>
    <article>
        <header>
            <h1>My Go Journey</h1>
        </header>
        <p>I decided to start learning Go in March 2017.</p>
        <p>Follow my journey through this new blog.</p>
    </article>
    <ul>
        <li><a href="/posts/post-01/">Post 1</a></li>
        <li><a href="/posts/post-02/">Post 2</a></li>
    </ul>
</main>
<!--bottom of your baseof-->
```

### 没有 `_index.md` 的列表页面 

​	您不必为每个列表页面（即章节、分类、分类术语等）或主页创建 `_index.md` 文件。如果 Hugo 在渲染列表模板时在相应的内容章节中找不到 `_index.md`，则将创建该页面，但没有 `{{ .Content }}`，只有 `.Title` 等的默认值。

​	将相同的 `layouts/_default/list.html` 模板应用于上面的 `quotes` 章节将渲染以下输出。请注意，`quotes` 没有可供提取的 `_index.md` 文件：

example.com/quote/index.html

```go-html-template
<!--baseof-->
<main>
    <article>
        <header>
        <!-- Hugo assumes that .Title is the name of the section since there is no _index.md content file from which to pull a "title:" field -->
            <h1>Quotes</h1>
        </header>
    </article>
    <ul>
        <li><a href="https://example.com/quote/quotes-01/">Quote 1</a></li>
        <li><a href="https://example.com/quote/quotes-02/">Quote 2</a></li>
    </ul>
</main>
<!--baseof-->
```

> 默认情况下，Hugo会将列表标题进行复数化处理，因此在使用 `.Title` [页面变量](https://gohugo.io/variables/page/)时，`quote`部分会变为"Quotes"。您可以通过在[站点配置](https://gohugo.io/getting-started/configuration/)中使用`pluralizeListTitles`指令来更改此设置。

## 示例列表模板 

### 章节模板 

​	这个列表模板是从[spf13.com](https://spf13.com/)的模板进行了略微修改。它使用[局部模板](https://gohugo.io/templates/partials/)来渲染页面的外壳，而不是使用[基础模板](https://gohugo.io/templates/base/)。下面的示例还使用了[内容视图模板](https://gohugo.io/templates/views/) `li.html` 或 `summary.html`。

layouts/section/posts.html

```go-html-template
{{ partial "header.html" . }}
{{ partial "subheader.html" . }}
<main>
  <div>
   <h1>{{ .Title }}</h1>
        <ul>
        <!-- Renders the li.html content view for each content/posts/*.md -->
            {{ range .Pages }}
                {{ .Render "li" }}
            {{ end }}
        </ul>
  </div>
</main>
{{ partial "footer.html" . }}
```

### 分类模板

layouts/_default/taxonomy.html

```go-html-template
{{ define "main" }}
<main>
  <div>
   <h1>{{ .Title }}</h1>
   <!-- ranges through each of the content files associated with a particular taxonomy term and renders the summary.html content view -->
    {{ range .Pages }}
        {{ .Render "summary" }}
    {{ end }}
  </div>
</main>
{{ end }}
```

## 内容排序 

​	Hugo 根据您在[前置元数据](https://gohugo.io/content-management/front-matter/)中提供的内容来渲染列表。除了合理的默认值外，Hugo 还提供了多种方法，以便在列表模板内快速进行内容排序：

### Default: Weight > Date > LinkTitle > FilePath 

layouts/partials/default-order.html

```go-html-template
<ul>
    {{ range .Pages }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按权重 

​	较低的权重具有较高的优先级。因此，权重较低的内容将排在前面。

layouts/partials/by-weight.html

```go-html-template
<ul>
    {{ range .Pages.ByWeight }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按日期

layouts/partials/by-date.html

```go-html-template
<ul>
    <!-- orders content according to the "date" field in front matter -->
    {{ range .Pages.ByDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按发布日期

layouts/partials/by-publish-date.html

```go-html-template
<ul>
    <!-- orders content according to the "publishdate" field in front matter -->
    {{ range .Pages.ByPublishDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按到期日期

layouts/partials/by-expiry-date.html

```go-html-template
<ul>
    {{ range .Pages.ByExpiryDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按最后修改日期

layouts/partials/by-last-mod.html

```go-html-template
<ul>
    <!-- orders content according to the "lastmod" field in front matter -->
    {{ range .Pages.ByLastmod }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按长度

layouts/partials/by-length.html

```go-html-template
<ul>
    <!-- orders content according to content length in ascending order (i.e., the shortest content will be listed first) -->
    {{ range .Pages.ByLength }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按标题

layouts/partials/by-title.html

```go-html-template
<ul>
    <!-- ranges through content in ascending order according to the "title" field set in front matter -->
    {{ range .Pages.ByTitle }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按链接标题

layouts/partials/by-link-title.html

```go-html-template
<ul>
    <!-- ranges through content in ascending order according to the "linktitle" field in front matter. If a "linktitle" field is not set, the range will start with content that only has a "title" field and use that value for .LinkTitle -->
    {{ range .Pages.ByLinkTitle }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

### 按参数

​	根据指定的前置元数据参数进行排序。如果内容没有指定的前置元数据字段，则使用站点的 `.Site.Params` 默认值。如果在某些条目中根本找不到该参数，这些条目将一起出现在排序的末尾。

layouts/partials/by-rating.html

```go-html-template
<!-- Ranges through content according to the "rating" field set in front matter -->
{{ range (.Pages.ByParam "rating") }}
  <!-- ... -->
{{ end }}
```

​	如果目标的前置元数据字段嵌套在另一个字段下，则您可以使用点表示法来访问该字段。

layouts/partials/by-nested-param.html

```go-html-template
{{ range (.Pages.ByParam "author.last_name") }}
  <!-- ... -->
{{ end }}
```

### 倒序排序 

​	可以将倒序排序应用于上述任何一种方法。以下示例以 `ByDate` 为例：

layouts/partials/by-date-reverse.html

```go-html-template
<ul>
    {{ range .Pages.ByDate.Reverse }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```

## 分组内容 

​	Hugo 提供一些函数，可按章节、类型、日期等对页面进行分组。

### 按页面字段

layouts/partials/by-page-field.html

```go-html-template
<!-- Groups content according to content section. The ".Key" in this instance will be the section's title. -->
{{ range .Pages.GroupBy "Section" }}
<h3>{{ .Key }}</h3>
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

​	在上面的例子中，您可能希望 `{{ .Title }}` 指向您已添加到 `_index.md` 文件中的`title`字段。您可以使用 [`.GetPage` 函数](https://gohugo.io/functions/getpage/)来访问此值：

layouts/partials/by-page-field.html

```go-html-template
<!-- Groups content according to content section.-->
{{ range .Pages.GroupBy "Section" }}
<!-- Checks for existence of _index.md for a section; if available, pulls from "title" in front matter -->
{{ with $.Site.GetPage "section" .Key }}
<h3>{{ .Title }}</h3>
{{ else }}
<!-- If no _index.md is available, ".Key" defaults to the section title and filters to title casing -->
<h3>{{ .Key | title }}</h3>
{{ end }}
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

### 按日期

layouts/partials/by-page-date.html

```go-html-template
<!-- Groups content by month according to the "date" field in front matter -->
{{ range .Pages.GroupByDate "2006-01" }}
<h3>{{ .Key }}</h3>
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

[在新版本 v0.97.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.97.0)，`GroupByDate` 函数接受与 [time.Format](https://gohugo.io/functions/dateformat/) 中相同的时间格式，并且结果中的 `.Key` 会根据当前语言进行本地化。

### 按发布日期

layouts/partials/by-page-publish-date.html

```go-html-template
<!-- Groups content by month according to the "publishDate" field in front matter -->
{{ range .Pages.GroupByPublishDate "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .PublishDate.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```

[在新版本 v0.97.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.97.0)，`GroupByDate` 函数接受与 [time.Format](https://gohugo.io/functions/dateformat/) 中相同的时间格式，并且结果中的 `.Key` 会根据当前语言进行本地化。



### 按照上次修改时间

layouts/partials/by-page-lastmod.html

```go-html-template
<!-- Groups content by month according to the "lastMod" field in front matter -->
{{ range .Pages.GroupByLastmod "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Lastmod.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```

[在新版本 v0.97.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.97.0)，`GroupByDate` 函数接受与 [time.Format](https://gohugo.io/functions/dateformat/) 中相同的时间格式，并且结果中的 `.Key` 会根据当前语言进行本地化。

### 按过期日期

layouts/partials/by-page-expiry-date.html

```go-html-template
<!-- Groups content by month according to the "expiryDate" field in front matter -->
{{ range .Pages.GroupByExpiryDate "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .ExpiryDate.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```

[在新版本 v0.97.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.97.0)，`GroupByDate` 函数接受与 [time.Format](https://gohugo.io/functions/dateformat/) 中相同的时间格式，并且结果中的 `.Key` 会根据当前语言进行本地化。

### 按照页面参数

layouts/partials/by-page-param.html

```go-html-template
<!-- Groups content according to the "param_key" field in front matter -->
{{ range .Pages.GroupByParam "param_key" }}
<h3>{{ .Key }}</h3>
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

### 按照页面参数和日期格式

​	在按`date`分组的模板中，使用了 Go 的布局字符串来进一步分组。有关如何使用 Go 的布局字符串格式化 Hugo 中的日期的更多示例，请参见 [Format 函数](https://gohugo.io/functions/format/)。

layouts/partials/by-page-param-as-date.html

```go-html-template
<!-- Groups content by month according to the "param_key" field in front matter -->
{{ range .Pages.GroupByParamDate "param_key" "2006-01" }}
<h3>{{ .Key }}</h3>
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

### 反向键顺序

​	分组的排序是按字母数字顺序的键进行排序（A-Z、1-100），并按照日期的逆序排列（即，最新的日期排在最前面）。

​	虽然这些是逻辑上的默认值，但并不总是期望的排序。有两种不同的语法可以更改 Hugo 的默认分组排序，它们都以相同的方式工作。

 

#### 1. 添加 Reverse 方法  

```go-html-template
{{ range (.Pages.GroupBy "Section").Reverse }}
{{ range (.Pages.GroupByDate "2006-01").Reverse }}
```

#### 2. 提供另一种方向 

```go-html-template
{{ range .Pages.GroupByDate "2006-01" "asc" }}
{{ range .Pages.GroupBy "Section" "desc" }}
```

### 组内排序

​	由于Grouping返回一个`{{ .Key }}`和一个页面片段，因此上述所有排序方法都可用。

​	以下是示例的排序方式：

1. 根据前置元数据中的`date`字段按月份分组内容。 
2. 按升序列出分组（即最旧的分组先列出）。 
3. 每个分组内的页面根据`title`按字母顺序排序。 

layouts/partials/by-group-by-page.html

```go-html-template
{{ range .Pages.GroupByDate "2006-01" "asc" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages.ByTitle }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```

## 筛选和限制列表 

​	有时，您只想列出可用内容的子集。一个常见的方法是仅在博客主页上显示主要章节的文章。

​	有关详细信息，请参见[where函数](https://gohugo.io/functions/where/)和[first函数](https://gohugo.io/functions/first/)的文档。

## 另请参阅

- [.GetPage](https://gohugo.io/functions/getpage/)
- [内容章节](https://gohugo.io/content-management/sections/)
- [内容类型](https://gohugo.io/content-management/types/)
- [菜单模板](https://gohugo.io/templates/menu-templates/)
- [分页](https://gohugo.io/templates/pagination/)
