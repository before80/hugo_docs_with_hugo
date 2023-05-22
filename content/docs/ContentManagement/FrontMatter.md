+++
title = "前置元数据"
weight = 5
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Front matter - 前置元数据 

[https://gohugo.io/content-management/front-matter/](https://gohugo.io/content-management/front-matter/)

​	Hugo 允许您在您的内容文件中添加 YAML、TOML 或 JSON 格式的前置元数据。 

​	前置元数据允许您将元数据附加到[内容类型](https://gohugo.io/content-management/types/)实例中，即嵌入在内容文件内部，这是 Hugo 赋予其强大功能的众多特点之一。

<iframe src="https://www.youtube.com/embed/Yh2xKRJGff4" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.984px; height: 305.977px; border: 0px;"></iframe>

## 前置元数据格式 

​	Hugo 支持四种前置元数据格式，每种格式都有其自己的标识符。

- TOML

  由打开和关闭 `+++` 标识。 

- YAML

  由打开和关闭 `---` 标识。 

- JSON

  由 '`{`' 和 '`}`' 包围的单个 JSON 对象，**后跟一个换行符**。 

- ORG

  ​	由一组以'`#+KEY: VALUE`'格式呈现的Org模式关键字组成。任何不以`#+`开头的行都会结束前置元数据部分。关键字值可以是字符串（`#+KEY: VALUE`）或空格分隔的字符串列表（`#+KEY[]: VALUE_1 VALUE_2`）。

### 示例

=== "yaml"

    ``` yaml
    categories:
    - Development
    - VIM
    date: "2012-04-06"
    description: spf13-vim is a cross platform distribution of vim plugins and resources
      for Vim.
    slug: spf13-vim-3-0-release-and-new-website
    tags:
    - .vimrc
    - plugins
    - spf13-vim
    - vim
    title: spf13-vim 3.0 release and new website
    ```

=== "toml"

    ``` toml
    categories = ['Development', 'VIM']
    date = '2012-04-06'
    description = 'spf13-vim is a cross platform distribution of vim plugins and resources for Vim.'
    slug = 'spf13-vim-3-0-release-and-new-website'
    tags = ['.vimrc', 'plugins', 'spf13-vim', 'vim']
    title = 'spf13-vim 3.0 release and new website'
    ```

=== "json"

    ``` json
    {
       "categories": [
          "Development",
          "VIM"
       ],
       "date": "2012-04-06",
       "description": "spf13-vim is a cross platform distribution of vim plugins and resources for Vim.",
       "slug": "spf13-vim-3-0-release-and-new-website",
       "tags": [
          ".vimrc",
          "plugins",
          "spf13-vim",
          "vim"
       ],
       "title": "spf13-vim 3.0 release and new website"
    }
    ```

## 前置元数据变量 

### 预定义 

​	有一些预定义变量是 Hugo 能够识别的。请参阅[页面变量](https://gohugo.io/variables/page/)以了解如何在模板中调用这些预定义变量。

- aliases

  一个由一个或多个别名（例如，已更名的内容的旧发布路径）组成的数组，这些别名将在输出目录结构中创建。详见[别名](https://gohugo.io/content-management/urls/#aliases)。 

- audio

  一个路径数组，用于与页面相关的音频文件；用于填充 `og:audio` 的 `opengraph` [内部模板](https://gohugo.io/templates/internal)。 

- cascade

  一个前置元数据键值对映射，其值会传递给页面的子代，除非被自身或更近的祖先级别的 cascade 覆盖。详见[前置元数据级联](https://gohugo.io/content-management/front-matter/#front-matter-cascade)。 

- date

  分配给此页面的日期时间。通常从前置元数据中的`date`字段获取，但此行为是可配置的。 

- description

  内容的描述。

- draft

  如果为 `true`，则不会渲染该内容，除非在 `hugo` 命令中传递 `--buildDrafts` 或 `-D`标志。 

- expiryDate

  内容应不再由 Hugo 发布的日期时间；除非在 `hugo` 命令中传递 `--buildExpired` 或`-E`标志，否则不会渲染已过期的内容。 

- headless

  如果为 `true`，则将叶子bundle设置为[headless](https://gohugo.io/content-management/page-bundles/#headless-bundle)。 

- images

  一个路径数组，用于与该页面相关的图像；用于[内部模板](https://gohugo.io/templates/internal)，例如 `_internal/twitter_cards.html`。 

- isCJKLanguage

  如果为 `true`，则 Hugo 将明确地将内容视为 CJK 语言；`.Summary` 和 `.WordCount` 在 CJK 语言中均能正常工作。 

- keywords

  该内容的元关键字。 

- layout

  在渲染内容时 Hugo 应从[查找顺序](https://gohugo.io/templates/lookup-order/)中选择的布局。如果在前置元数据中未指定`type`，则 Hugo 将在与内容所属章节对应的布局目录中查找同名的布局。请参阅[内容类型](https://gohugo.io/content-management/types/)。 

- lastmod

  该内容上次修改的日期时间。 

- linkTitle

  用于创建链接到内容；如果设置，则 Hugo 默认使用`title`之前的`linktitle`。Hugo 还可以按照`linktitle`对[内容列表进行排序](https://gohugo.io/templates/lists/#by-link-title)。

- markup

  实验性功能；指定`"rst"`表示使用reStructuredText（需要`rst2html`）或`"md"`（默认）表示使用Markdown。 

- outputs

  允许您指定特定于该内容的输出格式。请参见[输出格式](https://gohugo.io/templates/output-formats/)。 

- publishDate

  如果在将来，则不会呈现内容，除非传递`--buildFuture`或`-F`标志给`hugo`命令。 

- resources

  用于配置页面捆绑资源。请参见[页面资源](https://gohugo.io/content-management/page-resources/)。 

- series

  该页面属于的系列数组，作为`series`[分类法](https://gohugo.io/content-management/taxonomies/)的子集；被[内部模板](https://gohugo.io/templates/internal)`opengraph`用于填充`og:see_also`。 

- slug

  覆盖URL路径的最后一段。不适用于章节页面。有关详细信息，请参见[URL管理](https://gohugo.io/content-management/urls/#slug)。 

- summary

  在`.Summary`页面变量中提供文章摘要时使用的文本；有关详细信息，请参见[内容摘要](https://gohugo.io/content-management/summaries/)部分。 

- title

  该内容的标题。 

- type

  该内容的类型；如果在前置元数据中未指定，则该值将自动从目录（即[章节](https://gohugo.io/content-management/sections/)）派生。 

- url

  覆盖整个URL路径。适用于常规页面和章节页面。有关详细信息，请参见[URL管理](https://gohugo.io/content-management/urls/#url)。 

- videos

  页面相关视频路径的数组；被[内部模板](https://gohugo.io/templates/internal)`opengraph`用于填充`og:video`。 

- weight

  用于[在列表中排序内容](https://gohugo.io/templates/lists/)。**较低的权重具有更高的优先级**。因此，具有较低权重的内容将首先出现。如果设置了权重，则权重应为非零，因为0会被解释为未设置权重。 

- `<taxonomies>`

  索引的复数形式的字段名称。请参见上面的前置元数据示例中的`tags`和`categories`。请注意，用户定义的分类法（taxonomies）的复数形式不能与任何预定义的前置元数据变量相同。 

> ​	如果 `slug` 和 `url` 都不存在，并且[在您的站点配置文件中未配置永久链接](https://gohugo.io/content-management/urls/#permalinks)，Hugo 将使用您的内容文件名来创建输出 URL。请参见 Hugo 中的[内容组织](https://gohugo.io/content-management/organization)以了解 Hugo 中路径的说明，以及 [URL 管理](https://gohugo.io/content-management/urls/)以了解自定义 Hugo 的默认行为的方式。
>

### 用户自定义 

​	您可以任意添加字段到您的前置元数据中以满足您的需求。这些用户自定义的键值被放入一个`.Params`变量中，以供在您的模板中使用。

​	以下字段可以通过`.Params.include_toc`和`.Params.show_comments`进行访问。[变量](https://gohugo.io/variables/)章节提供有关在模板中使用Hugo的页面级别和站点级别变量的更多信息。

=== "yaml"

    ``` yaml
    include_toc: true
    show_comments: false
    ```

=== "toml"

    ``` toml
    include_toc = true
    show_comments = false
    ```

=== "json"

    ``` json
    {
       "include_toc": true,
       "show_comments": false
    }
    ```

## 前置元数据级联 

​	只要在保留的`cascade`前置元数据键下定义，任何节点或章节都可以向后代传递一组前置元数据值。

### 目标特定页面 

The `cascade` block can be a slice with a optional `_target` keyword, allowing for multiple `cascade` values targeting different page sets.

​	`cascade`块可以是一个切片，其中包含一个可选的`_target`关键字，允许多个`cascade`值针对不同的页面集。

=== "yaml"

    ``` yaml
    cascade:
    - _target:
        kind: page
        lang: en
        path: /blog/**
      background: yosemite.jpg
    - _target:
        kind: section
      background: goldenbridge.jpg
    title: Blog
    ```

=== "toml"

    ``` toml
    title = 'Blog'
    [[cascade]]
    background = 'yosemite.jpg'
    [cascade._target]
      kind = 'page'
      lang = 'en'
      path = '/blog/**'
    [[cascade]]
    background = 'goldenbridge.jpg'
    [cascade._target]
      kind = 'section'
    ```

=== "json"

    ``` json
    {
       "cascade": [
          {
             "_target": {
                "kind": "page",
                "lang": "en",
                "path": "/blog/**"
             },
             "background": "yosemite.jpg"
          },
          {
             "_target": {
                "kind": "section"
             },
             "background": "goldenbridge.jpg"
          }
       ],
       "title": "Blog"
    }
    ```

​	可用于`_target`的关键字：

- path

  匹配`/content`下的内容路径的[通配符](https://github.com/gobwas/glob)模式。期望是Unix风格的斜杠。注意，这是虚拟路径，因此它从挂载根开始。匹配支持双星号，因此您可以匹配模式如`/blog/*/**`，以匹配从第三层及以下的任何内容。 

- kind

  匹配该页面种类的通配符模式，例如"{home, section}"。 

- lang

  匹配该页面语言的通配符模式，例如"{en, sv}"。 

- environment

  匹配构建环境的通配符模式，例如"{production, development}"

​	以上任何一个都可以省略。

### 示例

在 `content/blog/_index.md`

=== "yaml"

    ``` yaml
    cascade:
      banner: images/typewriter.jpg
    title: Blog
    ```

=== "toml"

    ``` toml
    title = 'Blog'
    [cascade]
      banner = 'images/typewriter.jpg'
    ```

=== "json"

    ``` json
    {
       "cascade": {
          "banner": "images/typewriter.jpg"
       },
       "title": "Blog"
    }
    ```

在上面的示例中，除非：

- 该子页面已经设置了自己的`banner`值 
- 或更近的祖先节点已经设置了自己的`cascade.banner`值

否则博客章节页面和其后代页面将在调用`.Params.banner`时将返回`images/typewriter.jpg`。



## 通过前置元数据对内容进行排序 

​	您可以在内容的前置元数据中分配特定于内容的`weight`。这些值对于列表视图中的[排序](https://gohugo.io/templates/lists/)非常有用。您可以使用`weight`对内容进行排序，使用[<TAXONOMY>`_weight`](https://gohugo.io/content-management/taxonomies/)的约定对分类法（taxonomy）内的内容进行排序。请参阅[对有序列表进行排序和分组](https://gohugo.io/templates/lists/#order-content)，以了解如何使用`weight`在列表视图中组织您的内容。

## 覆盖全局 Markdown 配置 

​	可以在内容的前置元数据中设置某些Markdown渲染选项，作为[对项目配置中设置的Rendering选项](https://gohugo.io/getting-started/configuration/)的覆盖。

## 前置元数据格式规范 

- [TOML 规范](https://github.com/toml-lang/toml)
- [YAML 规范](https://yaml.org/spec/)
- [JSON 规范](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)

## 另请参阅 

- [原型 ](https://gohugo.io/content-management/archetypes/)
- [配置 Hugo ](https://gohugo.io/getting-started/configuration/)
- [数据模板 ](https://gohugo.io/templates/data-templates/)
- [Taxonomies](https://gohugo.io/content-management/taxonomies/)
- [Taxonomy Templates](https://gohugo.io/templates/taxonomy-templates/)
