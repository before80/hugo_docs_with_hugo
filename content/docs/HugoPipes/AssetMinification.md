+++
title = "压缩"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Minify - 压缩

[https://gohugo.io/hugo-pipes/minification/](https://gohugo.io/hugo-pipes/minification/)

​	压缩给定的资源。  

## 语法

```
resources.Minify RESOURCE
minify RESOURCE
```

## 用法 

​	任何 CSS、JS、JSON、HTML、SVG 或 XML 资源都可以使用  `resources.Minify`  进行压缩，该函数需要资源对象作为参数。

```go-html-template
{{ $css := resources.Get "css/main.css" }}
{{ $style := $css | resources.Minify }}
```

​	请注意，您也可以通过运行  `hugo --minify`  压缩最终的 HTML 输出到  `/public` 。  

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
- [FromString](https://gohugo.io/hugo-pipes/resource-from-string/)
