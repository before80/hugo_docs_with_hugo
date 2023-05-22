+++
title = "页面变量"
weight = 2
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Page Variables - 页面变量 

[https://gohugo.io/variables/page/](https://gohugo.io/variables/page/)

​	页面级变量定义在内容文件的前置元数据中，从内容文件的位置中派生出来，或从内容本身中提取出来。

​	以下是页面级变量列表。其中许多将在前置元数据中定义、从文件位置中派生或从内容本身中提取。

## 页面变量 

### .AlternativeOutputFormats

包含给定页面的所有备选格式；这个变量在您站点的 `<head>` 中的 `link rel` 列表中非常有用。（请参见[输出格式(Output Formats)](https://gohugo.io/templates/output-formats/)。）

### .Aliases

此页面的别名 

### .Ancestors

​	获取每个页面的祖先，简化 [面包屑导航(breadcrumb navigation)](https://gohugo.io/content-management/sections#example-breadcrumb-navigation) 实现的复杂性。

### .BundleType

​	[bundle](https://gohugo.io/content-management/page-bundles)类型: `leaf`, `branch`, 或者如果页面不是bundle，则为空字符串。

### .Content

​	内容本身，在前置元数据下定义。

### .Data

​	特定于此页面类型的数据。 

### .Date

​	与页面相关联的日期；`.Date`从内容的前置元数据中的`date`字段获取。还请参见`.ExpiryDate`、`.PublishDate`和`.Lastmod`。

### .Description

​	此页面的描述。

### .Draft

​	一个布尔值，如果内容在前置元数据中标记为草稿，则为 `true`。

### .ExpiryDate

​	内容计划过期的日期；`.ExpiryDate`从内容的前置元数据中的`expirydate`字段获取。还请参见`.PublishDate`、`.Date`和`.Lastmod`。

### .File

此内容文件的文件系统相关数据。另请参见[文件变量(File Variables)](https://gohugo.io/variables/files/)。

### .Fragments

​	Fragments返回此页面的片段。请参见[页面片段(Page Fragments)](https://gohugo.io/variables/page/#page-fragments)。

### .FuzzyWordCount

​	此内容中字的大致数量。

### .IsHome

​	在 [主页(homepage)](https://gohugo.io/templates/homepage/) 的上下文中为 `true`。

### .IsNode

​	对于常规内容页面始终为 `false`。

### .IsPage

​	对于常规内容页面始终为 `true`。

### .IsSection

​	如果 [`.Kind`](https://gohugo.io/templates/section-templates/#page-kinds) 是 `section`，则为 `true`。

### .IsTranslated

​	如果有要显示的翻译，则为 `true`。

### .Keywords

​	此内容的元关键字。

### .Kind

​	此页面的 *kind*。可能的返回值为 `page`、`home`、`section`、`taxonomy` 或 `term`。请注意，还有 `RSS`、`sitemap`、`robotsTXT` 和 `404` 类型，但这些仅在每个相应页面类型的渲染期间可用，因此这些不可在任何 `Pages` 集合中使用。

### .Language

​	一个指向该站点 `config` 中语言定义的语言对象。`.Language.Lang` 给出语言代码。

### .Lastmod

​	此内容最后修改日期。`.Lastmod` 从内容的前置元数据中的 `lastmod` 字段获取。

- 如果未设置 `lastmod` 并且 `.GitInfo` 特性已禁用，则将使用前置元数据中的 `date` 字段。
- 如果未设置 `lastmod` 并且 `.GitInfo` 特性已启用，则将使用`.GitInfo.AuthorDate`。

​	另请参阅 `.ExpiryDate`、`.Date`、`.PublishDate` 和 [.GitInfo](https://gohugo.io/variables/git/)。

### .LinkTitle

​	创建指向此内容的链接时使用。如果设置了（`linktitle`），Hugo 将在`title`之前使用前置元数据中的 `linktitle`。 

### .Next

​	指向下一个 [常规页面](https://gohugo.io/variables/site/#site-pages)（按 Hugo 的 [默认排序](https://gohugo.io/templates/lists#default-weight--date--linktitle--filepath) 排序）。示例：`{{ with .Next }}{{ .Permalink }}{{ end }}`。从第一页调用 `.Next` 将返回 `nil`。

### .NextInSection

​	指向同一顶级章节的下一个 [常规页面](https://gohugo.io/variables/site/#site-pages)（例如在 `/blog` 中）。页面按 Hugo 的 [默认排序](https://gohugo.io/templates/lists#default-weight--date--linktitle--filepath) 排序。示例：`{{ with .NextInSection }}{{ .Permalink }}{{ end }}`。从第一页调用 `.NextInSection` 将返回 `nil`。

### .OutputFormats

​	包含给定页面的所有格式，包括当前格式。可以与 [`.Get` 函数](https://gohugo.io/functions/get/) 结合使用来获取特定格式（请参阅 [输出格式](https://gohugo.io/templates/output-formats/)）。

### .Pages

​	相关页面的集合。在常规内容页面的上下文中，此值将为 `nil`。请参阅 [.Pages](https://gohugo.io/variables/page/#pages)。 

### .Permalink

​	此页面的永久链接；请参阅 [永久链接](https://gohugo.io/content-management/urls/)。

### .Plain

​	此页面内容去掉 HTML 标签后以字符串形式呈现。在使用 HTML [输出格式](https://gohugo.io/templates/output-formats#output-format-definitions) 渲染此值时，您可能需要通过 [`htmlUnescape`](https://gohugo.io/functions/htmlunescape/) 函数进行结果处理。

### .PlainWords

​	将 `.Plain` 拆分为字所生成的字符串切片，如 Go 的 [strings.Fields](https://pkg.go.dev/strings#Fields) 中定义。

### .Prev

​	指向上一个 [常规页面](https://gohugo.io/variables/site/#site-pages)（按 Hugo 的 [默认排序](https://gohugo.io/templates/lists#default-weight--date--linktitle--filepath) 排序）。示例：`{{ if .Prev }}{{ .Prev.Permalink }}{{ end }}`。从最后一页调用 `.Prev` 将返回 `nil`。

### .PrevInSection

​	指向同一顶级章节的下一个 [常规页面](https://gohugo.io/variables/site/#site-pages)（例如 `/blog`）。页面按 Hugo 的 [默认排序](https://gohugo.io/templates/lists#default-weight--date--linktitle--filepath) 排序。示例：`{{ if .PrevInSection }}{{ .PrevInSection.Permalink }}{{ end }}`。从最后一页调用 `.PrevInSection` 将返回 `nil`。

### .PublishDate

​	此内容发布日期或将要发布的日期；`.Publishdate` 从内容的前置元数据中的 `publishdate` 字段获取。另请参阅 `.ExpiryDate`、`.Date` 和 `.Lastmod`。

### .RawContent

​	没有前置元数据的原始Markdown内容。与 [remarkjs.com](https://remarkjs.com/) 配合使用很有用。 

### .ReadingTime

​	估计阅读此内容需要的时间（以分钟为单位）。

### .Resources

​	与此页面相关联的资源，例如图像和CSS。

### .Ref

​	返回给定引用（例如 `.Ref "sample.md"`）的永久链接。`.Ref` 无法正确处理页面内部片段。请参阅 [交叉引用](https://gohugo.io/content-management/cross-references/)。

### .RelPermalink

​	此页面的相对永久链接。

### .RelRef

​	返回给定引用（例如 `RelRef "sample.md"`）的相对永久链接。`.RelRef` 无法正确处理页面内部片段。请参阅 [交叉引用](https://gohugo.io/content-management/cross-references/)。

### .Site

​	参见[站点变量](https://gohugo.io/variables/site/)。 

### .Sites

​	返回所有站点（语言）。一个典型的用例是链接回主语言：`<a href="{{ .Sites.First.Home.RelPermalink }}">...</a>`。

### .Sites.First

​	返回第一种语言的站点。如果这不是多语言设置，则会返回它本身。

### .Summary

​	此内容的生成摘要，用于在摘要视图中轻松显示片段。可以在内容页中适当位置插入 `<!--more-->` 来手动设置断点，或者可以独立于页面文本编写摘要。有关详细信息，请参阅 [内容摘要](https://gohugo.io/content-management/summaries/)。

### .TableOfContents

​	此页面的渲染 [目录](https://gohugo.io/content-management/toc/)。

### .Title

​	此页面的标题。

### .Translations

​	当前页面的翻译版本列表。有关更多信息，请参阅 [多语言模式](https://gohugo.io/content-management/multilingual/)。

### .TranslationKey

​	用于映射当前页面的语言翻译的key。有关更多信息，请参阅 [多语言模式](https://gohugo.io/content-management/multilingual/)。

### .Truncated

​	一个布尔值，如果 `.Summary` 被截断，则为 `true`。仅在必要时显示"Read more…"链接很有用。有关详细信息，请参阅 [摘要](https://gohugo.io/content-management/summaries/)。

### .Type

​	此内容的 [内容类型](https://gohugo.io/content-management/types/)（例如 `posts`）。

### .Weight

​	分配给此内容的权重（在前置元数据中），用于排序。

### .WordCount

​	此内容中的字数。 

## 可写的页面范围变量 

### .Scratch

- [.Scratch](https://gohugo.io/functions/scratch)

  返回一个 Scratch 来存储和操作数据。与 [.Store](https://gohugo.io/functions/store) 方法相比，此 Scratch 在服务器重新构建时会被重置。

### .Store

- [.Store](https://gohugo.io/functions/store)

  返回一个 Scratch 来存储和操作数据。与 [.Scratch](https://gohugo.io/functions/scratch) 方法相比，此 Scratch 在服务器重新构建时不会被重置。

## 章节变量和方法 

​	另请参见[章节](https://gohugo.io/content-management/sections/)。

### .CurrentSection

​	此页面的当前章节。如果它是一个章节或主页，则该值可以是页面本身。 

### .FirstSection

​	此页面根目录下的第一个章节，例如 `/docs`、`/blog` 等等。

### .InSection $anotherPage

​	给定页面是否在当前章节中。

### .IsAncestor $anotherPage

​	当前页面是否是给定页面的祖先页面。

### .IsDescendant $anotherPage

​	当前页面是否是给定页面的后代页面。

### .Parent

​	章节的父级章节或页面所属的章节。

### .Section

​	此内容所属的[章节](https://gohugo.io/content-management/sections/)。**注意：** 对于嵌套章节，这是目录中的第一个路径元素，例如 `/blog/funny/mypost/ => blog`。

### .Sections

​	此内容下的[章节](https://gohugo.io/content-management/sections/)。

## `.Pages`变量 

​	`.Pages` 是 `.Data.Pages` 的别名。惯例是使用别名形式 `.Pages`。

### `.Pages`与`.Site.Pages`的比较 

- 常规页面是"post"页面或"content"页面。

  - 叶子bundle是常规页面。 

- 列表页面可以列出常规页面和其他列表页面。一些例子是：主页、章节页面、分类法（`/tags/`）和条目（`/tags/foo/`）页面。

  - 分支bundle是一个列表页面。 

- `.Site.Pages`

  站点中**所有**页面的集合：常规页面、章节、分类法等等。——Superset of everything!

- `.Site.RegularPages`

  仅包含常规页面的集合。

​	上述`.Site. ..`页面集合可以从模板的任何作用域中访问。

​	以下变量仅从当前列表页的作用域返回页面集合：

- `.Pages`

  Collection of *regular* pages and *only first-level* section pages under the current *list* page.

  在当前列表页面下，包含所有常规页面和**只有一级**章节页面的集合。 

- `.RegularPages`

  仅包括当前*列表*页面下的常规页面的集合。这**不包括**嵌套章节/列表页面中的常规页面（那些是带有 `_index.md` 文件的子目录）。

- `.RegularPagesRecursive`

  包含一个*列表*页面下的所有*普通*页面的集合。这**包括**嵌套章节/*列表*页面中的常规页面。

  > 注意
  >
  > 从*常规*页面的作用域来看，`.Pages` 和 `.RegularPages` 返回一个空的 slice。

## Page Fragments 页面片段 

[New in v0.111.0](https://github.com/gohugoio/hugo/releases/tag/v0.111.0)

​	`.Fragments` 方法返回当前页面的片段列表。

### .Headings

​	当前页面的递归标题列表。可用于生成目录。

### .Identifiers

​	当前页面的标识符的排序列表。可用于检查页面是否包含特定标识符或页面是否包含重复标识符：

```go-html-template
{{ if .Fragments.Identifiers.Contains "my-identifier" }}
    <p>Page contains identifier "my-identifier"</p>
{{ end }}

{{ if gt (.Fragments.Identifiers.Count "my-identifier")  1 }}
    <p>Page contains duplicate "my-identifier" fragments</p>
{{ end }}
```

### .HeadingsMap

​	保存了当前页面的一个标题映射。可用于从特定标题开始生成目录。

​	还请参阅 [Go Doc](https://pkg.go.dev/github.com/gohugoio/hugo@v0.111.0/markup/tableofcontents#Fragments) 获取返回类型的信息。

### hooks和简码中的Fragments 

​	`.Fragments` 可以在渲染钩子中安全调用，即使在当前页面（`.Page.Fragments`）上也可以。对于简码，我们建议所有 `.Fragments` 的用法都嵌套在 `\{\{\<\>\}\}` 简码定界符内（`\{\{\%\%\}\}` 参与 ToC 的创建，所以很容易陷入一种咬尾巴的情况）。

## 全局页面函数 

[New in v0.111.1](https://github.com/gohugoio/hugo/releases/tag/v0.111.1)

​	Hugo 几乎总是将 `Page` 作为数据上下文传递到顶层模板（例如 `single.html`）中（唯一的例外是多主机（multihost ）站点地图模板）。这意味着您可以在模板中使用 `.` 变量访问当前页面。

​	但是，在 `.Render`，partial 等嵌套较深的情况下，访问该 `Page` 对象并不总是实用或可能的。

​	因此，Hugo 提供了一个全局的 `page` 函数，您可以使用它从任何模板中的任何位置访问当前页面。

```go-html-template
{{ page.Title }}
```

​	这里有一个需要注意的地方，这并不是新问题，但是值得在这里提一下：在 Hugo 中，您可能会看到缓存值的情况，例如在 `partialCached` 或简码中时。

## Page-level Params 

​	在内容文件中定义的任何其他值，包括分类法，都将作为 `.Params` 变量的一部分提供。

content/example.md

=== "yaml"

    ``` yaml
    ---
    categories:
    - one
    tags:
    - two
    - three
    - four
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    categories = ['one']
    tags = ['two', 'three', 'four']
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "categories": [
          "one"
       ],
       "tags": [
          "two",
          "three",
          "four"
       ],
       "title": "Example"
    }
    ```



​	使用上面的前置元数据，可以通过以下方式访问 `tags` 和 `categories` 分类法：

- `.Params.tags`
- `.Params.categories`

​	`.Params` 变量对于在内容文件中引入用户定义的前置元数据字段特别有用。例如，针对图书评论的 Hugo 站点可以具有以下前置元数据：

content/example.md

=== "yaml"

    ``` yaml
    ---
    affiliatelink: http://www.my-book-link.here
    recommendedby: My Mother
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    affiliatelink = 'http://www.my-book-link.here'
    recommendedby = 'My Mother'
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "affiliatelink": "http://www.my-book-link.here",
       "recommendedby": "My Mother",
       "title": "Example"
    }
    ```



​	然后可以通过 `.Params.affiliatelink` 和 `.Params.recommendedby` 访问这些字段。

```go-html-template
<h3><a href="{{ .Params.affiliatelink }}">Buy this book</a></h3>
<p>It was recommended by {{ .Params.recommendedby }}.</p>
```

​	该模板将被渲染成如下：

```html
<h3><a href="http://www.my-book-link.here">Buy this book</a></h3>
<p>It was recommended by my Mother.</p>
```

​	有关在每篇内容之间保持 `Params` 的一致性，请参见 [Archetypes](https://gohugo.io/content-management/archetypes/)。

### `.Param`方法 

​	在 Hugo 中，您可以针对个别页面和整个站点全局声明参数。一个常见的用例是为站点参数设置一个通用值，为一些页面设置更具体的值（例如，头像图片）：

```go-html-template
{{ $.Param "header_image" }}
```

​	`.Param` 方法提供了一种解析单个值的方式，根据它在页面参数（即内容的前置条件）或站点参数（即您的 `config`）中的定义。

### 访问前置元数据中的嵌套字段

​	当前置元数据包含类似以下的嵌套字段时：

content/example.md

=== "yaml"

    ` yaml
    ---
    author:
      display_name: John Feminella
      family_name: Feminella
      given_name: John
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    title = 'Example'
    [author]
      display_name = 'John Feminella'
      family_name = 'Feminella'
      given_name = 'John'
    +++
    ```

=== "json"

    ``` json
    {
       "author": {
          "display_name": "John Feminella",
          "family_name": "Feminella",
          "given_name": "John"
       },
       "title": "Example"
    }
    ```



​	`.Param` 可以通过连接字段名称并用点号分隔来访问这些字段：

```go-html-template
{{ $.Param "author.display_name" }}
```

## 另请参阅  

- [Pages方法](https://gohugo.io/variables/pages/)
