+++
title = "FromString"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# FromString

[https://gohugo.io/hugo-pipes/resource-from-string/](https://gohugo.io/hugo-pipes/resource-from-string/)

​	从字符串创建资源。  

## 语法

```
resources.FromString TARGET_PATH CONTENT
```

## 用法 

​	可以使用  `resources.FromString`  直接从模板创建资源，该函数需要两个参数，即要创建资源的目标路径和给定的内容字符串。  

​	下面的示例创建一个包含每个项目语言的本地化变量的资源文件。

```go-html-template
{{ $string := (printf "var rootURL = '%s'; var apiURL = '%s';" (absURL "/") (.Param "API_URL")) }}
{{ $targetPath := "js/vars.js" }}
{{ $vars := $string | resources.FromString $targetPath }}
{{ $global := resources.Get "js/global.js" | resources.Minify }}

<script src="{{ $vars.Permalink }}"></script>
<script src="{{ $global.Permalink }}"></script>
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
- [Minify](https://gohugo.io/hugo-pipes/minification/)
