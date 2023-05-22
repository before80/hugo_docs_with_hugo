+++
title = "Index"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# index

[https://gohugo.io/functions/index-function/](https://gohugo.io/functions/index-function/)

Looks up the index(es) or key(s) of the data structure passed into it.

## 语法

```
index COLLECTION INDEXES
index COLLECTION KEYS
```

The `index` functions returns the result of indexing its first argument by the following arguments. Each indexed item must be a map or a slice, e.g.:

```go-text-template
{{ $slice := slice "a" "b" "c" }}
{{ index $slice 1 }} => b
{{ $map := dict "a" 100 "b" 200 }}
{{ index $map "b" }} => 200
```

The function takes multiple indices as arguments, and this can be used to get nested values, e.g.:

```go-text-template
{{ $map := dict "a" 100 "b" 200 "c" (slice 10 20 30) }}
{{ index $map "c" 1 }} => 20
{{ $map := dict "a" 100 "b" 200 "c" (dict "d" 10 "e" 20) }}
{{ index $map "c" "e" }} => 20
```

You may write multiple indices as a slice:

```go-text-template
{{ $map := dict "a" 100 "b" 200 "c" (dict "d" 10 "e" 20) }}
{{ $slice := slice "c" "e" }}
{{ index $map $slice }} => 20
```

## Example: Load Data from a Path Based on Front Matter Params 

Assume you want to add a `location = ""` field to your front matter for every article written in `content/vacations/`. You want to use this field to populate information about the location at the bottom of the article in your `single.html` template. You also have a directory in `data/locations/` that looks like the following:

```
.
└── data
    └── locations
        ├── abilene.toml
        ├── chicago.toml
        ├── oslo.toml
        └── provo.toml
```

Here is an example:

data/locations/oslo.

=== "yaml"

    ``` yaml
    pop_city: 658390
    pop_metro: 1717900
    website: https://www.oslo.kommune.no
    ```

=== "toml"

    ``` toml
    pop_city = 658390
    pop_metro = 1717900
    website = 'https://www.oslo.kommune.no'
    ```

=== "json"

    ``` json
    {
       "pop_city": 658390,
       "pop_metro": 1717900,
       "website": "https://www.oslo.kommune.no"
    }
    ```



The example we will use will be an article on Oslo, whose front matter should be set to exactly the same name as the corresponding file name in `data/locations/`:

content/articles/oslo.md

=== "yaml"

    ``` yaml
    ---
    location: oslo
    title: My Norwegian Vacation
    ---
    ```

=== "toml"

    ``` toml
    +++
    location = 'oslo'
    title = 'My Norwegian Vacation'
    +++
    ```

=== "json"

    ``` json
    {
       "location": "oslo",
       "title": "My Norwegian Vacation"
    }
    ```



The content of `oslo.toml` can be accessed from your template using the following node path: `.Site.Data.locations.oslo`. However, the specific file you need is going to change according to the front matter.

This is where the `index` function is needed. `index` takes 2 parameters in this use case:

1. The node path
2. A string corresponding to the desired data; e.g.—

```go-html-template
{{ index .Site.Data.locations "oslo" }}
```

The variable for `.Params.location` is a string and can therefore replace `oslo` in the example above:

```go-html-template
{{ index .Site.Data.locations .Params.location }}
=> map[website:https://www.oslo.kommune.no pop_city:658390 pop_metro:1717900]
```

Now the call will return the specific file according to the location specified in the content’s front matter, but you will likely want to write specific properties to the template. You can do this by continuing down the node path via dot notation (`.`):

```go-html-template
{{ (index .Site.Data.locations .Params.location).pop_city }}
=> 658390
```
