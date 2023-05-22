+++
title = "分类法"
weight = 13
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Taxonomies - 分类法

[https://gohugo.io/content-management/taxonomies/](https://gohugo.io/content-management/taxonomies/)

​	Hugo支持用户定义的分类法。

## 什么是分类法？ 

​	Hugo支持用户定义的内容分组，称为**分类法（taxonomies）**。分类法是内容之间逻辑关系的分类。

### 定义 

- Taxonomy

  可用于对内容进行分类的分类方式 

- Term

  分类法中的一个键 

- Value

  分配给项(term)的内容 

## 示例分类法：电影站点 

​	假设您正在制作一个关于电影的站点。您可能想包括以下分类法：

- Actors 演员 
- Directors 导演
- Studios 制片厂
- Genre 流派
- Year 年份
- Awards 奖项

​	然后，在每部电影中，您都需要为这些分类法指定项（即，在每部电影的内容文件的[前置元数据](https://gohugo.io/content-management/front-matter/)中）。根据这些项（terms），Hugo会自动创建每个Actor、Director、Studio、Genre、Year和Award的页面，每个页面都会列出与特定Actor、Director、Studio、Genre、Year和Award匹配的所有电影。

### 电影分类法组织 

​	继续使用电影站点的示例，以下演示了从分类法的角度看内容关系：

```txt
Actor                    <- Taxonomy
    Bruce Willis         <- Term
        The Sixth Sense  <- Value
        Unbreakable      <- Value
        Moonrise Kingdom <- Value
    Samuel L. Jackson    <- Term
        Unbreakable      <- Value
        The Avengers     <- Value
        xXx              <- Value
```

​	从内容的角度看，关系看起来不同，尽管使用的数据和标签是相同的：

```txt
Unbreakable                 <- Value
    Actors                  <- Taxonomy
        Bruce Willis        <- Term
        Samuel L. Jackson   <- Term
    Director                <- Taxonomy
        M. Night Shyamalan  <- Term
    ...
Moonrise Kingdom            <- Value
    Actors                  <- Taxonomy
        Bruce Willis        <- Term
        Bill Murray         <- Term
    Director                <- Taxonomy
        Wes Anderson        <- Term
    ...
```

## Hugo分类法默认设置 

​	Hugo本身支持分类法。

​	不需要在您的[站点配置](https://gohugo.io/getting-started/configuration/)文件中添加任何行，Hugo将自动为`tags`和`categories`创建分类法。这与[手动配置您的分类法](https://gohugo.io/content-management/taxonomies/#configure-taxonomies)相同，如下所示：

config.

=== "yaml"

    ``` yaml
    taxonomies:
      category: categories
      tag: tags
    ```

=== "toml"

    ``` toml
    [taxonomies]
      category = 'categories'
      tag = 'tags'
    ```

=== "json"

    ``` json
    {
       "taxonomies": {
          "category": "categories",
          "tag": "tags"
       }
    }
    ```

​	如果您不想让Hugo创建任何分类法，请将[站点配置](https://gohugo.io/getting-started/configuration/)中的`disableKinds`设置为以下内容：

config.

=== "yaml"

    ``` yaml
    disableKinds:
    - taxonomy
    - term
    ```

=== "toml"

    ``` toml
    disableKinds = ['taxonomy', 'term']
    
    ```

=== "json"

    ``` json
    {
       "disableKinds": [
          "taxonomy",
          "term"
       ]
    }
    
    ```



| Kind       | Description          | Example                                                      |
| :--------- | :------------------- | :----------------------------------------------------------- |
| `home`     | 主页的着陆页         | `/index.html`                                                |
| `page`     | 给定页面的着陆页     | `my-post` page (`/posts/my-post/index.html`)                 |
| `section`  | 给定章节的着陆页     | `posts` section (`/posts/index.html`)                        |
| `taxonomy` | 分类法的着陆页       | `tags` taxonomy (`/tags/index.html`)                         |
| `term`     | 一个分类法项的着陆页 | term `awesome` in `tags` taxonomy (`/tags/awesome/index.html`) |

### 默认目标 

​	当使用分类法并提供[分类法模板](https://gohugo.io/templates/taxonomy-templates/)时，Hugo将自动创建列出所有分类法项的页面以及列出与每个项关联的内容的个别页面。例如，在您的配置中声明并在内容前置元数据中使用的`categories`分类法将创建以下页面：

- 位于`example.com/categories/`的单个页面，列出[分类法中的所有项](https://gohugo.io/templates/taxonomy-templates/#taxonomy-terms-templates) 
- 为每个项创建的[单独的分类法列表页面](https://gohugo.io/templates/taxonomy-templates/)（例如`/categories/development/`），其中显示了所有标记为该分类法的任何内容文件的[前置元数据](https://gohugo.io/content-management/front-matter/)中的页面列表 

## 配置分类法 

​	除了[默认](https://gohugo.io/content-management/taxonomies/#default-taxonomies)之外的自定义分类法在整个站点中使用之前必须在[站点配置](https://gohugo.io/getting-started/configuration/)中定义。您需要为每个分类法提供复数和单数标签。例如，对于TOML，`singular key = "plural value"`，而对于YAML，`singular key: "plural value"`。

### 示例：添加名为"series"的自定义分类法 

> 在添加自定义分类法时，如果您想保留它们，您需要同时添加默认分类法。
>

config.

=== "yaml"

    ``` yaml
    taxonomies:
      category: categories
      series: series
      tag: tags
    ```

=== "toml"

    ``` toml
    [taxonomies]
      category = 'categories'
      series = 'series'
      tag = 'tags'
    ```

=== "json"

    ``` json
    {
       "taxonomies": {
          "category": "categories",
          "series": "series",
          "tag": "tags"
       }
    }
    ```



### 示例：删除默认分类法 

​	如果您只想要默认`tags`分类法，并删除您站点的`categories`分类法，可以通过修改[站点配置](https://gohugo.io/getting-started/configuration/)文件中的`taxonomies`值来实现。

config.

=== "yaml"

    ``` yaml
    taxonomies:
      tag: tags
    ```

=== "toml"

    ``` toml
    [taxonomies]
      tag = 'tags'
    ```

=== "json"

    ``` json
    {
       "taxonomies": {
          "tag": "tags"
       }
    }
    ```



​	如果您想要完全禁用所有分类法，请参阅 [Hugo 分类法默认设置](https://gohugo.io/content-management/taxonomies/#default-taxonomies)中 `disableKinds` 的用法。

> ​	您可以向您的分类法列表和分类法项页面添加内容和前置元数据。有关如何为此目的添加 `_index.md` 的更多信息，请参见[内容组织](https://gohugo.io/content-management/organization/)。
>
> ​	与常规页面类似，分类法列表[永久链接](https://gohugo.io/content-management/urls/)是可配置的，但分类法项页面永久链接是不可配置的。
>

> ​	Hugo 0.55 版中删除了配置选项 `preserveTaxonomyNames`。
>
> ​	现在，您可以在相关分类法节点（taxonomy node）上使用 `.Page.Title` 来获取原始值。
>

## 将分类法添加到内容中 

​	一旦在站点级别定义了分类法，任何内容都可以被分配给它，而不管[内容类型](https://gohugo.io/content-management/types/)或[内容章节](https://gohugo.io/content-management/sections/)。

​	将内容分配给分类法是在[前置元数据](https://gohugo.io/content-management/front-matter/)中完成的。只需创建一个变量，其名称为taxonomy 的复数形式，并分配所有要应用于内容类型实例的项。

> ​	如果您希望能够快速生成具有预配置分类法或项的内容文件，请阅读有关 [Hugo 原型](https://gohugo.io/content-management/archetypes/)的文档。

### 示例：带有taxonomies 的前置元数据 

content/example.md

=== "yaml"

    ``` yaml
    ---
    categories:
    - Development
    project_url: https://github.com/gohugoio/hugo
    series:
    - Go Web Dev
    slug: hugo
    tags:
    - Development
    - Go
    - fast
    - Blogging
    title: 'Hugo: A fast and flexible static site generator'
    ---
    ```

=== "toml"

    ``` toml
    +++
    categories = ['Development']
    project_url = 'https://github.com/gohugoio/hugo'
    series = ['Go Web Dev']
    slug = 'hugo'
    tags = ['Development', 'Go', 'fast', 'Blogging']
    title = 'Hugo: A fast and flexible static site generator'
    +++
    ```

=== "json"

    ``` json
    {
       "categories": [
          "Development"
       ],
       "project_url": "https://github.com/gohugoio/hugo",
       "series": [
          "Go Web Dev"
       ],
       "slug": "hugo",
       "tags": [
          "Development",
          "Go",
          "fast",
          "Blogging"
       ],
       "title": "Hugo: A fast and flexible static site generator"
    }
    ```



## 排序分类法 

​	内容文件可以为其关联的每个分类法分配权重。分类法权重可用于在[分类法列表模板](https://gohugo.io/templates/taxonomy-templates/#taxonomy-list-templates)中排序或排序内容，并在内容文件的[前置元数据](https://gohugo.io/content-management/front-matter/)中声明。声明分类法权重的约定是`taxonomyname_weight`。

​	以下显示一个具有权重为22的内容，可在渲染分配给`tags`分类法的"a"、"b"和"c"值的页面时用于排序目的。在渲染"d"类别页面时，它也被分配了权重44。

### 示例：分类法`weight`

=== "yaml"

    ``` yaml
    categories:
    - d
    categories_weight: 44
    tags:
    - a
    - b
    - c
    tags_weight: 22
    title: foo
    ```

=== "toml"

    ``` toml
    categories = ['d']
    categories_weight = 44
    tags = ['a', 'b', 'c']
    tags_weight = 22
    title = 'foo'
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
       "title": "foo"
    }
    ```



​	通过使用分类法权重，同一篇内容可以在不同的分类法中出现在不同的位置。

> ​	目前，分类法仅支持[默认`weight => date`排序列表内容](https://gohugo.io/templates/lists/#default-weight--date--linktitle--filepath)。有关更多信息，请参见[分类法模板](https://gohugo.io/templates/taxonomy-templates/)的文档。

## 向分类法或项添加自定义元数据 

​	如果您需要向分类法项添加自定义元数据，则需要在 `/content/<TAXONOMY>/<TERM>/_index.md` 中创建该项的页面，并在其前置元数据中添加您的元数据。继续以'Actors'为例，假设您想为每个演员添加维基百科页面链接。您的分类项页面将如下所示：

content/actors/bruce-willis/_index.md

=== "yaml"

    ``` yaml
    ---
    title: Bruce Willis
    wikipedia: https://en.wikipedia.org/wiki/Bruce_Willis
    ---
    ```

=== "toml"

    ``` toml
    +++
    title = 'Bruce Willis'
    wikipedia = 'https://en.wikipedia.org/wiki/Bruce_Willis'
    +++
    ```

=== "json"

    ``` json
    {
       "title": "Bruce Willis",
       "wikipedia": "https://en.wikipedia.org/wiki/Bruce_Willis"
    }
    ```



## 另请参阅 

- [分类法模板 ](https://gohugo.io/templates/taxonomy-templates/)
- [原型 ](https://gohugo.io/content-management/archetypes/)
- [前置元数据 ](https://gohugo.io/content-management/front-matter/)
- [Hugo 中的内容列表 ](https://gohugo.io/templates/lists/)
- [.Param](https://gohugo.io/functions/param/)
