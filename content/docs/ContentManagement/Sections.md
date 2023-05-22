+++
title = "内容章节"
weight = 11
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Content Sections - 内容章节 

[https://gohugo.io/content-management/sections/](https://gohugo.io/content-management/sections/)

​	Hugo 生成与您的内容匹配的章节树。 

​	章节是根据 `content/` 目录下的组织结构定义的页面集合。

​	默认情况下，`content/` 下的**所有一级目录**都形成自己的章节（根章节），前提是它们构成[分支 Bundles](https://gohugo.io/content-management/page-bundles/#branch-bundles)。即使是一级目录，如果它们只是[叶子 Bundles](https://gohugo.io/content-management/page-bundles/#leaf-bundles)，也不会形成自己的章节。

​	如果用户需要在更深的层次上定义一个名为 `foo` 的章节，则需要创建一个名为 `foo` 的目录，并包含一个 `_index.md` 文件（有关更多信息，请参见[分支 Bundles](https://gohugo.io/content-management/page-bundles/#branch-bundles)）。

​	章节不能通过前置元数据参数进行定义或覆盖——它严格基于内容组织结构派生。

## 嵌套章节 

​	章节可以嵌套到任意深度。

```bash
content
└── blog        <-- Section, 因为是content/目录下的一级目录
    ├── funny-cats
    │   ├── mypost.md
    │   └── kittens         <-- Section, 因为包含 _index.md
    │       └── _index.md
    └── tech                <-- Section, 因为包含 _index.md
        └── _index.md
```

​	理解的重要部分是，为了使章节树完全可导航，至少需要一个内容文件作为最低层的章节（例如 `_index.md`）。

​	当我们谈论与模板选择相关的章节时，目前仅涉及根章节（`/blog/funny-cats/mypost/ => blog`）。

​	如果您需要一个子章节的特定模板，则需要在前置元数据参数中调整`type`或`layout`。

## 示例：面包屑导航 

​	通过可用的[章节变量和方法](https://gohugo.io/content-management/sections/#section-page-variables-and-methods)，您可以构建强大的导航。其中一个常见的示例是使用部分（partial ）来显示面包屑导航：

layouts/partials/breadcrumb.html

```go-html-template
<nav aria-label="breadcrumb">
  <ol>
    {{ range .Ancestors.Reverse }}
      <li>
        <a href="{{ .Permalink }}">{{ .LinkTitle }}</a>
      </li>
    {{ end }}
    <li class="active">
      <a aria-current="page" href="{{ .Permalink }}">{{ .LinkTitle }}</a>
    </li>
  </ol>
</nav>
```

## 章节页面变量和方法 

​	另请参见[页面变量](https://gohugo.io/variables/page/)。

- .CurrentSection

  该页面所属的当前章节。如果该页面本身就是章节或主页，则该值可以是该页面本身。 

- .FirstSection

  根目录下该页面的第一级章节，例如`/docs`、`/blog` 等。 

- .InSection $anotherPage

  给定页面是否在当前章节中。 

- .IsAncestor $anotherPage

  当前页面是否是给定页面的祖先。 

- .IsDescendant $anotherPage

  当前页面是否是给定页面的后代。 

- .Parent

  一个章节的父章节或一个页面所属的章节。 

- .Section

  该内容所属的章节。注意：对于被嵌套章节，这是目录中的第一个路径元素，例如 `/blog/funny/mypost/ => blog`。 

- .Sections

  此内容下面的章节。 


## 内容章节列表 

​	Hugo 将为每个**根章节**自动创建一个页面，列出该章节中的所有内容。有关自定义这些页面的渲染方式的详细信息，请参见[章节模板](https://gohugo.io/templates/section-templates/)文档。

## 内容章节与内容类型 

​	默认情况下，创建在章节中的所有内容都将使用与根章节名称相匹配的[内容`type`](https://gohugo.io/content-management/types/)。例如，Hugo 将假定 `posts/post-1.md` 具有 `posts` 内容`type`。如果您正在使用 `post` 章节的[原型](https://gohugo.io/content-management/archetypes/)，Hugo 将根据在 `archetypes/posts.md` 中找到的内容生成前置元数据。

## 另请参阅  

- [内容类型 ](https://gohugo.io/content-management/types/)
- [.GetPage](https://gohugo.io/functions/getpage/)
- [评论](https://gohugo.io/content-management/comments/)
- [内容组织 ](https://gohugo.io/content-management/organization/)
- [Hugo 中的内容列表](https://gohugo.io/templates/lists/)
