+++
title = "分页"
weight = 18
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Pagination - 分页 

​	Hugo支持对主页、章节页面和分类目录进行分页。 

​	Hugo分页功能真正的强大之处在于与[`where`函数](https://gohugo.io/functions/where/)及其类似SQL的操作符：`first`、`last`和`after`相结合使用。您甚至可以按照Hugo中熟悉的方式对[内容进行排序](https://gohugo.io/templates/lists/)。

## 配置分页 

​	可以在[站点配置](https://gohugo.io/getting-started/configuration/)中配置分页：

- `paginate`

  默认值为`10`。这个设置可以在模板中被覆盖。 

- `paginatePath`

  默认值为`page`。允许您为您的分页页面设置不同的路径。 

​	将`paginate`设置为正值将把主页、章节和分类列表页面拆分为这个大小的块。但是请注意，对于章节、分类和主页的分页页面的生成是惰性的——如果没有通过`.Paginator`引用，这些页面将不会被创建（见下文）。

​	`paginatePath`用于调整分页器中页面的`URL`（默认设置会生成这样的URL形式`/page/1/`）。

## 列出分页器页面 

​	提供`.Paginator`帮助您构建分页器菜单。此功能目前仅在主页和列表页面（即分类和章节列表）上受支持。

​	有两种配置和使用`.Paginator`的方法：

1. 最简单的方法是只需从模板中调用`.Paginator.Pages`。它将包含该页面的页面。 
2. 使用可用的模板函数和排序选项选择另一组页面，并将切片传递给`.Paginate`，例如 

- `{{ range (.Paginate ( first 50 .Pages.ByTitle )).Pages }}` 或
- `{{ range (.Paginate .RegularPagesRecursive).Pages }}`.

​	对于给定的页面，它是上面选项之一。`.Paginator`是静态的，一旦创建就不能更改。

​	如果在同一页中多次调用 `.Paginator` 或 `.Paginate`，您应该确保所有调用都是相同的。一旦在生成页面时调用了 `.Paginator` 或 `.Paginate`，其结果就会被缓存，任何后续相似的调用都将重用缓存的结果。这意味着任何不符合第一个调用的这种调用都不会按预期行事。

（请记住，函数参数是急切地求值的，因此像 `$paginator := cond x .Paginator (.Paginate .RegularPagesRecursive)` 这样的调用就是您不应该做的事情。请使用 `if/else` 确保恰好有一个求值。）

​	全局页面大小设置（`Paginate`）可以通过提供正整数作为最后一个参数来覆盖。下面的示例将每页显示五个项：

- `{{ range (.Paginator 5).Pages }}`
- `{{ $paginator := .Paginate (where .Pages "Type" "posts") 5 }}`

也可以将 `GroupBy` 函数与分页结合使用：

```go-html-template
{{ range (.Paginate (.Pages.GroupByDate "2006")).PageGroups }}
```

## 构建导航 

​	`.Paginator` 包含构建分页界面所需的足够信息。

​	将内置模板（具有与 Bootstrap 兼容的样式）包含到您的页面中是添加此内容的最简单方法：

```go-html-template
{{ template "_internal/pagination.html" . }}
```

​	如果使用任何过滤器或排序函数来创建您的 `.Paginator`，并且您希望在显示页面列表之前显示导航按钮，则必须在使用之前创建 `.Paginator`。

​	以下示例显示如何在使用 `.Paginator` 之前创建 `.Paginator`：

```go-html-template
{{ $paginator := .Paginate (where .Pages "Type" "posts") }}
{{ template "_internal/pagination.html" . }}
{{ range $paginator.Pages }}
   {{ .Title }}
{{ end }}
```

​	如果没有 `where` 过滤器，则上面的示例更加简单：

```go-html-template
{{ template "_internal/pagination.html" . }}
{{ range .Paginator.Pages }}
   {{ .Title }}
{{ end }}
```

​	如果您想要构建自定义的导航菜单，您可以使用`.Paginator`对象，它包括以下属性：

- `PageNumber`

  当前页面在页面序列中的页码 

- `URL`

  当前页面器的相对URL 

- `Pages`

  当前页面器中的页面 

- `NumberOfElements`

  此页面中的元素数量 

- `HasPrev`

  当前页之前是否有页 

- `Prev`

  前一页的分页器 

- `HasNext`

  当前页之后是否有页 

- `Next`

  下一页的分页器 

- `First`

  第一页的分页器 

- `Last`

  最后一页的分页器 

- `Pagers`

  可用于构建分页菜单的分页器列表 

- `PageSize`

  每个分页器的大小 

- `TotalPages`
  

  分页器中的页面数 

- `TotalNumberOfElements`

  此分页器中所有页面上的元素数

## 附加信息 

​	页面按以下形式构建（`BLANK`表示没有值）：

```txt
[SECTION/TAXONOMY/BLANK]/index.html
[SECTION/TAXONOMY/BLANK]/page/1/index.html => redirect to  [SECTION/TAXONOMY/BLANK]/index.html
[SECTION/TAXONOMY/BLANK]/page/2/index.html
....
```

## 另请参阅  

- [.GetPage](https://gohugo.io/functions/getpage/)
- [内容章节](https://gohugo.io/content-management/sections/)
- [内容类型 ](https://gohugo.io/content-management/types/)
- [在Hugo中的内容列表 ](https://gohugo.io/templates/lists/)
- [菜单模板](https://gohugo.io/templates/menu-templates/)
