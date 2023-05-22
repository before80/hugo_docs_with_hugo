+++
title = "Union"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# union

[https://gohugo.io/functions/union/](https://gohugo.io/functions/union/)

Given two arrays or slices, returns a new array that contains the elements or objects that belong to either or both arrays/slices.

## 语法

```
union SET1 SET2
```

Given two arrays (or slices) A and B, this function will return a new array that contains the elements or objects that belong to either A or to B or to both. The elements supported are strings, integers, and floats (only float64).

```go-html-template
{{ union (slice 1 2 3) (slice 3 4 5) }}
<!-- returns [1 2 3 4 5] -->

{{ union (slice 1 2 3) nil }}
<!-- returns [1 2 3] -->

{{ union nil (slice 1 2 3) }}
<!-- returns [1 2 3] -->

{{ union nil nil }}
<!-- returns an error because both arrays/slices have to be of the same type -->
```

## OR filter in where query 

This is also very useful to use as `OR` filters when combined with where:

```go-html-template
{{ $pages := where .Site.RegularPages "Type" "not in" (slice "page" "about") }}
{{ $pages = $pages | union (where .Site.RegularPages "Params.pinned" true) }}
{{ $pages = $pages | intersect (where .Site.RegularPages "Params.images" "!=" nil) }}
```

The above fetches regular pages not of `page` or `about` type unless they are pinned. And finally, we exclude all pages with no `images` set in Page params.

See [intersect](https://gohugo.io/functions/intersect) for `AND`.

## 另请参阅

- [intersect](https://gohugo.io/functions/intersect/)
- [symdiff](https://gohugo.io/functions/symdiff/)
- [append](https://gohugo.io/functions/append/)
- [complement](https://gohugo.io/functions/complement/)
- [group](https://gohugo.io/functions/group/)
