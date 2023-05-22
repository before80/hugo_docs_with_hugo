+++
title = "站点变量"
weight = 1
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Site Variables - 站点变量 

[https://gohugo.io/variables/site/](https://gohugo.io/variables/site/)

​	许多站点范围的变量在站点配置中定义，但是，Hugo提供了许多内置变量，以方便在模板中访问全局值。 

​	以下是站点级别（也称为"全局"）变量列表。其中许多变量在[站点配置](https://gohugo.io/getting-started/configuration/)文件中定义，而其他变量则内置于Hugo的核心中，以便在模板中方便使用。

## 从局部获取Site对象 

​	下面的所有方法，例如`.Site.RegularPages`也可以通过全局[`site`函数](https://gohugo.io/functions/site/)（例如`site.RegularPages`）访问，这在局部文件中 `Page` 对象不容易获取时可能会很方便。

## 站点变量列表 

### .Site.AllPages

​	所有页面的数组，不考虑它们的翻译。 

### .Site.BaseURL

​	站点配置中定义的站点基本URL。

### .Site.BuildDrafts

​	一个布尔值（默认值为`false`），用于指示是否按照站点配置构建草稿。

### .Site.Copyright

​	表示您的站点版权的字符串，即在站点配置中所定义的。 

### .Site.Data

​	自定义数据，请参阅[数据模板](https://gohugo.io/templates/data-templates/)。 

### .Site.DisqusShortname

​	表示Disqus简码的字符串，即在站点配置文件中所定义的。

### .Site.GoogleAnalytics

​	表示Google Analytics追踪代码的字符串，即在站点配置文件中所定义的。

### .Site.Home

​	指向主页[页面对象](https://gohugo.io/variables/page/)的引用。

### .Site.IsMultiLingual

​	是否在该站点中存在多种语言。有关更多信息，请参见[多语言](https://gohugo.io/content-management/multilingual/)。 

### .Site.IsServer

​	一个布尔值，指示是否使用Hugo的内置服务器提供站点。有关更多信息，请参见[hugo server](https://gohugo.io/commands/hugo_server/)。

### .Site.Language.Lang

​	当前区域设置的语言代码（例如，`en`）。 

### .Site.Language.LanguageName

​	完整的语言名称（例如，`English`）。 

### .Site.Language.Weight

​	定义`.Site.Languages`列表顺序的权重。 

### .Site.Language

​	指示当前用于渲染站点的语言。该对象的属性在站点配置语言定义中设置。 

### .Site.LanguageCode

​	表示在站点配置中定义的语言tag的字符串。 

### .Site.LanguagePrefix

​	可以用于为URL添加前缀以指向正确的语言。即使只定义了一种语言，它也会起作用。另请参见[absLangURL](https://gohugo.io/functions/abslangurl/)和[relLangURL](https://gohugo.io/functions/rellangurl)函数。

### .Site.Languages

​	一个按照定义的权重排序的语言列表。

### .Site.LastChange

​	一个表示站点最近更改的日期/时间的字符串。此字符串基于内容页面[前置元数据](https://gohugo.io/content-management/front-matter)中的`date`变量。

### .Site.Menus

​	站点中的所有菜单。

### .Site.Pages

​	按日期排序的所有内容的数组，最新的在前面。此数组仅包含当前语言的页面。请参阅[.Site.Pages](https://gohugo.io/variables/site/#site-pages)。

### .Site.RegularPages

​	一个常规页面集合的快捷方式。`.Site.RegularPages`等效于`where .Site.Pages "Kind" "page"`。请参阅[.Site.Pages](https://gohugo.io/variables/site/#site-pages)。

### .Site.Sections

​	站点的顶级目录。

### .Site.Taxonomies

​	  整个站点的分类法。另请参阅[从任何模板访问分类法数据](https://gohugo.io/variables/taxonomy/#access-taxonomy-data-from-any-template)的章节。

### .Site.Title

  ​	一个表示站点标题的字符串。

## `.Site.Params`变量 

​	`.Site.Params`是一个容器，它保存了来自站点配置`params` 部分的值。

### 示例： `.Site.Params` 

​	以下`config.[yaml|toml|json]`定义了一个站点范围的`description`参数：

config.

=== "yaml"

    ``` yaml
    baseURL: https://yoursite.example.com/
    params:
      author: Nikola Tesla
      description: Tesla's Awesome Hugo Site
    ```

=== "toml"

    ``` toml
    baseURL = 'https://yoursite.example.com/'
    [params]
      author = 'Nikola Tesla'
      description = "Tesla's Awesome Hugo Site"
    ```

=== "json"

    ``` json
    {
       "baseURL": "https://yoursite.example.com/",
       "params": {
          "author": "Nikola Tesla",
          "description": "Tesla's Awesome Hugo Site"
       }
    }
    ```



​	您可以在[局部模板](https://gohugo.io/templates/partials/)中使用`.Site.Params`调用默认站点描述：

layouts/partials/head.html

```go-html-template
<meta name="description" content="{{ if .IsHome }}{{ $.Site.Params.description }}{{ else }}{{ .Description }}{{ end }}" />
```

## .Site.Pages变量 

### `.Site.Pages`与`.Pages`比较

- 常规页面是"post"页面或"content"页面。 

  - 叶子bundle是常规页面。 

- 列表页面可以列出常规页面和其他列表页面。一些示例是：主页、章节页面、分类法(`/tags/`)和条目(`/tags/foo/)`页面。 

  - 分支bundle是列表页面。

- `.Site.Pages`

  站点所有页面的集合：常规页面、章节页面、分类法页面等——Superset of everything!

- `.Site.RegularPages`

  仅包含常规页面的集合。

​	上述`.Site. ..`页面集合可以从模板的任何作用域中访问。

​	以下变量仅从当前列表页的作用域返回页面集合：

- `.Pages`

  Collection of *regular* pages and *only first-level* section pages under the current *list* page.

  在当前列表页面下，包含所有常规页面和**只有一级**章节页面的集合。

- `.RegularPages`

  仅包含当前*列表*页面下的*普通*页面的集合。这**排除**嵌套章节/*列表*页面中的常规页面（那些是带有 `_index.md` 文件的子目录）。

- `.RegularPagesRecursive`

  包含一个*列表*页面下的所有*普通*页面的集合。这**包括**嵌套章节/*列表*页面中的常规页面。

  

  > 注意
  >
  > 从*常规*页面的作用域来看，`.Pages` 和 `.RegularPages` 返回一个空的 slice。
