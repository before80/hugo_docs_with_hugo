+++
title = "ExecuteAsTemplate"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# ExecuteAsTemplate

[https://gohugo.io/hugo-pipes/resource-from-template/](https://gohugo.io/hugo-pipes/resource-from-template/)

​	从模板创建资源。  

## 语法

```
resources.ExecuteAsTemplate TARGET_PATH CONTEXT RESOURCE
```

## 用法 

​	为了在包含 Go 模板的一个asset 文件上使用 Hugo Pipes 函数，必须使用  `resources.ExecuteAsTemplate`  函数。  

​	 该函数需要三个参数：创建资源的目标路径、模板上下文和资源对象。

```go-html-template
// assets/sass/template.scss
$backgroundColor: {{ .Param "backgroundColor" }};
$textColor: {{ .Param "textColor" }};
body{
  background-color:$backgroundColor;
  color: $textColor;
}
// [...]
{{ $sassTemplate := resources.Get "sass/template.scss" }}
{{ $style := $sassTemplate | resources.ExecuteAsTemplate "main.scss" . | resources.ToCSS }}
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
- [FromString](https://gohugo.io/hugo-pipes/resource-from-string/)
- [Minify](https://gohugo.io/hugo-pipes/minification/)
