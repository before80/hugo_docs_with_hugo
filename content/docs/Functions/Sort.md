+++
title = "Sort"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# sort

[https://gohugo.io/functions/sort/](https://gohugo.io/functions/sort/)

Sorts slices, maps, and page collections.

## 语法

```
sort COLLECTION [KEY] [ORDER]
```

The `KEY` is optional when sorting slices in ascending order, otherwise it is required. When sorting slices, use the literal `value` in place of the `KEY`. See examples below.

The `ORDER` may be either `asc` (ascending) or `desc` (descending). The default sort order is ascending.

## Sort a slice 

The examples below assume this site configuration:

config.

=== "yaml"

    ``` yaml
    params:
      grades:
      - b
      - a
      - c
    ```

=== "toml"

    ``` toml
    [params]
      grades = ['b', 'a', 'c']
    ```

=== "json"

    ``` json
    {
       "params": {
          "grades": [
             "b",
             "a",
             "c"
          ]
       }
    }
    ```



### Ascending order 

Sort slice elements in ascending order using either of these constructs:

layouts/_default/single.html

```go-html-template
{{ sort site.Params.grades }} → [a b c]
{{ sort site.Params.grades "value" "asc" }} → [a b c]
```

In the examples above, `value` is the `KEY` representing the value of the slice element.

### Descending order 

Sort slice elements in descending order:

layouts/_default/single.html

```go-html-template
{{ sort site.Params.grades "value" "desc" }} → [c b a]
```

In the example above, `value` is the `KEY` representing the value of the slice element.

## Sort a map 

The examples below assume this site configuration:

config.

=== "yaml"

    ``` yaml
    params:
      authors:
        a:
          firstName: Marius
          lastName: Pontmercy
        b:
          firstName: Victor
          lastName: Hugo
        c:
          firstName: Jean
          lastName: Valjean
    ```

=== "toml"

    ``` toml
    [params]
      [params.authors]
        [params.authors.a]
          firstName = 'Marius'
          lastName = 'Pontmercy'
        [params.authors.b]
          firstName = 'Victor'
          lastName = 'Hugo'
        [params.authors.c]
          firstName = 'Jean'
          lastName = 'Valjean'
    ```

=== "json"

    ``` json
    {
       "params": {
          "authors": {
             "a": {
                "firstName": "Marius",
                "lastName": "Pontmercy"
             },
             "b": {
                "firstName": "Victor",
                "lastName": "Hugo"
             },
             "c": {
                "firstName": "Jean",
                "lastName": "Valjean"
             }
          }
       }
    }
    ```



When sorting maps, the `KEY` argument must be lowercase.

### Ascending order 

Sort map objects in ascending order using either of these constructs:

layouts/_default/single.html

```go-html-template
{{ range sort site.Params.authors "firstname" }}
  {{ .firstName }}
{{ end }}

{{ range sort site.Params.authors "firstname" "asc" }}
  {{ .firstName }}
{{ end }}
```

These produce:

```text
Jean Marius Victor
```

### Descending order 

Sort map objects in descending order:

layouts/_default/single.html

```go-html-template
{{ range sort site.Params.authors "firstname" "desc" }}
  {{ .firstName }}
{{ end }}
```

This produces:

```text
Victor Marius Jean
```

## Sort a page collection 

Although you can use the `sort` function to sort a page collection, Hugo provides [built-in methods for sorting page collections](https://gohugo.io/templates/lists/#order-content) by:

- weight
- linktitle
- title
- front matter parameter
- date
- expiration date
- last modified date
- publish date
- length

In this contrived example, sort the site’s regular pages by `.Type` in descending order:

layouts/_default/home.html

```go-html-template
{{ range sort site.RegularPages "Type" "desc" }}
  <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
{{ end }}
```

## 另请参阅

- [.GetPage](https://gohugo.io/functions/getpage/)
- [Content Sections](https://gohugo.io/content-management/sections/)
- [Content Types](https://gohugo.io/content-management/types/)
- [Lists of Content in Hugo](https://gohugo.io/templates/lists/)
- [Menu Templates](https://gohugo.io/templates/menu-templates/)
