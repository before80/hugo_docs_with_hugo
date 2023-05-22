+++
title = "First"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# first

[https://gohugo.io/functions/first/](https://gohugo.io/functions/first/)

Slices an array to only the first *N* elements.

## 语法

```
first LIMIT COLLECTION
```

`first` works in a similar manner to the [`limit` keyword in SQL](https://www.techonthenet.com/sql/select_limit.php). It reduces the array to only the `first N` elements. It takes the array and number of elements as input.

`first` takes two arguments:

1. `number of elements`
2. `array` *or* `slice of maps or structs`

layout/_default/section.html



```go-html-template
{{ range first 10 .Pages }}
    {{ .Render "summary" }}
{{ end }}
```

*Note: Exclusive to `first`, LIMIT can be ‘0’ to return an empty array.*

## `first` and `where` Together 

Using `first` and [`where`](https://gohugo.io/functions/where/) together can be very powerful. Below snippet gets a list of posts only from [**main sections**](https://gohugo.io/functions/where/#mainsections), sorts it by the `title` parameter, and then ranges through only the first 5 posts in that list:

first-and-where-together.html



```go-html-template
{{ range first 5 (where site.RegularPages "Type" "in" site.Params.mainSections).ByTitle }}
   {{ .Content }}
{{ end }}
```

## 另请参阅

- [.Scratch](https://gohugo.io/functions/scratch/)
- [after](https://gohugo.io/functions/after/)
- [delimit](https://gohugo.io/functions/delimit/)
- [range](https://gohugo.io/functions/range/)
