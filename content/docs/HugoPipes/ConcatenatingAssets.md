+++
title = "Concat"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Concat

https://gohugo.io/hugo-pipes/bundling/

​	将任意数量的assets捆绑成一个资源。  

## 语法

```
resources.Concat TARGET_PATH SLICE_RESOURCES
```

## 用法 

​	相同 MIME 类型的asset文件可以使用  `resources.Concat`  捆绑成一个资源，该函数需要两个参数，分别为创建资源捆绑的目标路径和要连接的资源对象的切片。

```go-html-template
{{ $plugins := resources.Get "js/plugins.js" }}
{{ $global := resources.Get "js/global.js" }}
{{ $js := slice $plugins $global | resources.Concat "js/bundle.js" }}
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
- [FromString](https://gohugo.io/hugo-pipes/resource-from-string/)
- [Minify](https://gohugo.io/hugo-pipes/minification/)
