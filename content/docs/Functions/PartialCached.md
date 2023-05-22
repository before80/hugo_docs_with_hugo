+++
title = "PartialCached"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# partialCached

[https://gohugo.io/functions/partialcached/](https://gohugo.io/functions/partialcached/)

Allows for caching of partials that do not need to be re-rendered on every invocation.

## 语法

```
partialCached LAYOUT INPUT [VARIANT...]
```

The `partialCached` template function can offer significant performance gains for complex templates that don’t need to be re-rendered on every invocation.

**Note:** Each Site (or language) has its own `partialCached` cache, so each site will execute a partial once.

**Note**: Hugo renders pages in parallel, and will render the partial more than once with concurrent calls to the `partialCached` function. After Hugo caches the rendered partial, new pages entering the build pipeline will use the cached result.

Here is the simplest usage:

```go-html-template
{{ partialCached "footer.html" . }}
```

You can also pass additional parameters to `partialCached` to create *variants* of the cached partial. For example, if you have a complex partial that should be identical when rendered for pages within the same section, you could use a variant based upon section so that the partial is only rendered once per section:

partial-cached-example.html



```go-html-template
{{ partialCached "footer.html" . .Section }}
```

If you need to pass additional parameters to create unique variants, you can pass as many variant parameters as you need:

```go-html-template
{{ partialCached "footer.html" . .Params.country .Params.province }}
```

Note that the variant parameters are not made available to the underlying partial template. They are only use to create a unique cache key. Since Hugo `0.61.0` you can use any object as cache key(s), not just strings.

See also [The Full Partial Series Part 1: Caching!](https://regisphilibert.com/blog/2019/12/hugo-partial-series-part-1-caching-with-partialcached/).

## 另请参阅

- [The Benefits of Static Site Generators](https://gohugo.io/about/benefits/)
