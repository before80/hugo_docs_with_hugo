+++
title = "构建选项"
weight = 6
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Build Options - 构建选项

[https://gohugo.io/content-management/build-options/](https://gohugo.io/content-management/build-options/)

​	构建选项有助于定义 Hugo 在构建站点时如何处理给定页面。

​	它们存储在名为 `_build` 的保留前置元数据对象中，具有以下默认值：

=== "yaml"

    ``` yaml
    _build:
      list: always
      publishResources: true
      render: always
    ```

=== "toml"

    ``` toml
    [_build]
      list = 'always'
      publishResources = true
      render = 'always'
    ```

=== "json"

    ``` json
    {
       "_build": {
          "list": "always",
          "publishResources": true,
          "render": "always"
       }
    }
    ```



#### render 

​	如果设置为 `always`，该页面将被视为已发布页面，并保留其专用输出文件（`index.html` 等）和永久链接。

​	我们从布尔值将此属性扩展为枚举，从 Hugo 0.76.0 开始，有效值包括：

- never

  该页面不会包含在任何页面集合中。 

- always (default)

  该页面将被渲染到磁盘并获得 `RelPermalink` 等。 

- link

  该页面不会被渲染到磁盘，但会获得 `RelPermalink`。

#### list 

​	请注意，我们从布尔值将此属性扩展为枚举，从 Hugo 0.68.0 开始，有效值包括：

- never

  该页面不会包含在任何页面集合中。 

- always (default)

  该页面将包含在所有页面集合中，例如 `site.RegularPages`、`$page.Pages`。 

- local

  该页面将包含在任何本地页面集合中，例如 `$page.RegularPages`、`$page.Pages`。其一个用例是创建完全可导航但无头内容章节。

​	如果为 `true`，则该页面将被视为项目集合的一部分，并在适当时通过 Hugo 的列表方法（`.Pages`、`.RegularPages` 等）返回。

#### publishResources 

​	如果设置为 `true`，则 [Bundle 的资源](https://gohugo.io/content-management/page-bundles)将被发布。将其设置为 `false` 将仍会按需发布资源（当从模板调用资源的 `.Permalink` 或 `.RelPermalink` 时），但会跳过其他资源。

> ​	无论其构建选项如何，任何页面都始终可以使用 `.GetPage` 方法访问。
>

### 说明性用例 

#### 不发布某个页面 

​	项目需要一个"Who We Are"内容文件，其中包括前置元数据和正文，用于主页但不用于其他任何地方。

content/who-we-are.md

=== "yaml"

    ``` yaml
    ---
    _build:
      list: false
      render: false
    title: Who we are
    ---
    ```

=== "toml"

    ``` toml
    +++
    title = 'Who we are'
    [_build]
      list = false
      render = false
    +++
    ```

=== "json"

    ``` json
    {
       "_build": {
          "list": false,
          "render": false
       },
       "title": "Who we are"
    }
    ```

layouts/index.html

```go-html-template
<section id="who-we-are">
  {{ with site.GetPage "who-we-are" }}
    {{ .Content }}
  {{ end }}
</section>
```

#### 列出未发布的页面 

​	站点需要展示一些可用的百余个"推荐（testimonials）"内容文件，而不发布其中任何一个。

​	为了避免在每个推荐中设置构建选项，可以在推荐章节的内容文件上使用`cascade`。

=== "yaml"

    ``` yaml
    _build:
      render: true
    cascade:
      _build:
        list: true
        render: false
    title: Testimonials
    ```

=== "toml"

    ``` toml
    title = 'Testimonials'
    [_build]
      render = true
    [cascade]
      [cascade._build]
        list = true
        render = false
    ```

=== "json"

    ``` json
    {
       "_build": {
          "render": true
       },
       "cascade": {
          "_build": {
             "list": true,
             "render": false
          }
       },
       "title": "Testimonials"
    }
    ```



layouts/_defaults/testimonials.html

```go-html-template
<section id="testimonials">
  {{ range first 5 .Pages }}
    <blockquote cite="{{ .Params.cite }}">
      {{ .Content }}
    </blockquote>
  {{ end }}
</section>
```

## 另请参阅

- [.Param](https://gohugo.io/functions/param/)
- [原型](https://gohugo.io/content-management/archetypes/)
- [评论](https://gohugo.io/content-management/comments/)
- [内容组织 ](https://gohugo.io/content-management/organization/)
- [前置元数据](https://gohugo.io/content-management/front-matter/)
