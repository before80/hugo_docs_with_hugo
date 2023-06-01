+++
title = ".GetPage"
weight = 4
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .GetPage

[https://gohugo.io/functions/getpage/](https://gohugo.io/functions/getpage/)

​	获取给定 `path` 的 `Page`。

## 语法

```
.GetPage PATH
```

​	`.GetPage` 返回给定 `path` 的页面。`Site` 和 `Page` 都实现了该方法。如果给定相对路径（即没有前导 `/` 的路径），`Page` 变量会尝试查找相对于当前页面的页面。

**注意：** 在 Hugo 0.45 中我们重新设计和简化了 `.GetPage` API。在此之前，除了路径，您还需要提供一个 `Kind` 属性，例如 `{{ .Site.GetPage "section" "blog" }}`。这仍然可以工作，但是现在是多余的（superfluous）。

```go-html-template
{{ with .Site.GetPage "/blog" }}{{ .Title }}{{ end }}
```

​	当找不到页面时，此方法将返回 `nil`，因此如果找不到blog章节，则上面的示例不会打印任何内容。

​	要在blog章节中查找一个常规页面：

```go-html-template
{{ with .Site.GetPage "/blog/my-post.md" }}{{ .Title }}{{ end }}
```

​	由于 `Page` 还提供了一个 `.GetPage` 方法，因此上述示例与以下示例相同：

```go-html-template
{{ with .Site.GetPage "/blog" }}
{{ with .GetPage "my-post.md" }}{{ .Title }}{{ end }}
{{ end }}
```

## `.GetPage` 和多语言站点

​	前面的示例使用了完整的内容文件名来查找帖子。根据您的内容组织方式（文件名中是否有语言代码，例如 `my-post.en.md`），您可能希望在没有扩展名的情况下进行查找。这将为您获取当前语言版本的页面：

```go-html-template
{{ with .Site.GetPage "/blog/my-post" }}{{ .Title }}{{ end }}
```

## `.GetPage` 示例

​	此代码片段（以[局部模板](https://gohugo.io/templates/partials/)的形式）允许您执行以下操作： 

1. 获取 `tags` [分类法](https://gohugo.io/content-management/taxonomies/)的索引对象。
2. 将该对象分配给变量 `$t`。
3. 按受欢迎程度排序与分类法相关联的条目。
4. 获取分类法中最受欢迎的两个条目（即分配给内容的两个最受欢迎的标签）。

grab-top-two-tags.html

```go-html-template
<ul class="most-popular-tags">
{{ $t := .Site.GetPage "/tags" }}
{{ range first 2 $t.Data.Terms.ByCount }}
    <li>{{ . }}</li>
{{ end }}
</ul>
```

## `.GetPage` 在页面bundle中

​	如果通过 `.GetPage` 检索到的页面是[Leaf Bundle](https://gohugo.io/content-management/page-bundles/#leaf-bundles)，并且您需要获取其中的嵌套**page**资源，则需要使用 `.Resources` 中的方法，如[Page Resources](https://gohugo.io/content-management/page-resources/)中所述。 

​	有关示例，请参见[Headless Bundle](https://gohugo.io/content-management/page-bundles/#headless-bundle)文档。 

## 另请参阅

- [Content Sections](https://gohugo.io/content-management/sections/)
- [Content Types](https://gohugo.io/content-management/types/)
- [Lists of Content in Hugo](https://gohugo.io/templates/lists/)
- [Menu Templates](https://gohugo.io/templates/menu-templates/)
- [Pagination](https://gohugo.io/templates/pagination/)
