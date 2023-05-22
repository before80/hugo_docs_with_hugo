+++
title = "原型"
weight = 12
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Archetypes - 原型

[https://gohugo.io/content-management/archetypes/](https://gohugo.io/content-management/archetypes/)

​	Archetypes是在创建新内容时使用的模板。 

## 什么是Archetypes？ 

​	Archetypes是位于项目的[archetypes目录](https://gohugo.io/getting-started/directory-structure/)中的内容模板文件，其中包含为您的站点[内容类型（content types）](https://gohugo.io/content-management/types/)预配置的[前置元数据（前置元数据）](https://gohugo.io/content-management/front-matter/)和可能的内容排列方式。当您运行`hugo new`时，将使用这些模板。

​	`hugo new`使用`content-section`来查找项目中最合适的原型模板。如果您的项目不包含任何原型文件，它也会在主题中查找。

archetype-example.sh

```sh
hugo new posts/my-first-post.md
```

​	以上将创建一个新的内容文件`content/posts/my-first-post.md`，使用找到的第一个原型文件:

1. `archetypes/posts.md`
2. `archetypes/default.md`
3. `themes/my-theme/archetypes/posts.md`
4. `themes/my-theme/archetypes/default.md`

​	最后两个列表项仅适用于您使用主题并且它使用`my-theme`主题名称作为示例。

## 创建新的Archetype模板 

​	以下是一个虚构的`newsletter` section 的示例，以及原型文件`archetypes/newsletter.md`。在`archetypes/`中创建一个新文件`newsletter.md`并在文本编辑器中打开它。

archetypes/newsletter.md

```md
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
---

**Insert Lead paragraph here.**

## New Cool Posts

{{ range first 10 ( where .Site.RegularPages "Type" "cool" ) }}
* {{ .Title }}
{{ end }}
```

​	当您使用以下命令创建新的newsletter：

```bash
hugo new newsletter/the-latest-cool.stuff.md
```

​	它将基于原型模板创建一个新的newsletter类型的内容文件。

!!! warning "注意"
	注意：如果在原型文件中使用了 `.Site`，那么只有在构建站点时才会构建。这对于大型站点可能需要很长时间。

​	上述`newsletter`类型的原型展示了可能性：完整的Hugo `.Site`和所有Hugo模板函数都可以在原型文件中使用。

## 基于目录的archetypes 

​	从Hugo `0.49`开始，您可以使用完整的目录作为原型模板。假设有以下原型目录：

```bash
archetypes
├── default.md
└── post-bundle
    ├── bio.md
    ├── images
    │   └── featured.jpg
    └── index.md

```

```bash
hugo new --kind post-bundle posts/my-post
```

​	该命令将创建一个新的文件夹`/content/posts/my-post`，并且它包含与`post-bundle`原型文件夹中相同的一组文件。所有内容文件（例如`index.md`）都可以包含模板逻辑，并将为内容的语言接收正确的`.Site`。

## 另请参阅 

- [前置元数据](https://gohugo.io/content-management/front-matter/)
- [Taxonomies](https://gohugo.io/content-management/taxonomies/)
- [Taxonomy Templates](https://gohugo.io/templates/taxonomy-templates/)
- [.Param](https://gohugo.io/functions/param/)
- [构建选项](https://gohugo.io/content-management/build-options/)
