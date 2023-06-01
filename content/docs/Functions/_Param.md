+++
title = ".Param"
weight = 8
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Param

[https://gohugo.io/functions/param/](https://gohugo.io/functions/param/)

​	返回一个页面参数，如果存在站点参数则返回站点参数。

## 语法

```
.Param KEY
```

​	`.Param` 方法在 `.Page` 对象中查找给定的 `KEY`，并返回对应的值。如果无法在页面参数中找到 `KEY`，则在站点参数中查找 `KEY`。如果两个位置都找不到 `KEY`，则 `.Param` 方法返回 `nil`。

​	站点和主题开发人员通常在站点级别设置参数，允许内容作者在页面级别上覆盖这些参数。

​	例如，要在每个页面上显示目录，但允许作者在需要时隐藏目录：

**Configuration**

config.

=== "yaml"

    ``` yaml
    params:
      display_toc: true
    ```

=== "toml"

    ``` toml
    [params]
      display_toc = true
    ```

=== "json"

    ``` json
    {
       "params": {
          "display_toc": true
       }
    }
    ```



**Content**

content/example.md

=== "yaml"

    ``` yaml
    ---
    date: "2023-01-01"
    display_toc: false
    draft: false
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    date = 2023-01-01
    display_toc = false
    draft = false
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "date": "2023-01-01",
       "display_toc": false,
       "draft": false,
       "title": "Example"
    }
    ```



**Template**

layouts/_default/single.html

```go-html-template
{{ if .Param "display_toc" }}
  {{ .TableOfContents }}
{{ end }}
```

​	`.Param`方法返回与给定`KEY`关联的值，无论该值是否为真值或假值。如果需要忽略假值，请改用此构造：

layouts/_default/single.html

```go-html-template
{{ or .Params.foo site.Params.foo }}
```

## 另请参阅

- [Archetypes](https://gohugo.io/content-management/archetypes/)
- [Build Options](https://gohugo.io/content-management/build-options/)
- [Front Matter](https://gohugo.io/content-management/front-matter/)
- [Taxonomies](https://gohugo.io/content-management/taxonomies/)
- [Taxonomy Templates](https://gohugo.io/templates/taxonomy-templates/)
