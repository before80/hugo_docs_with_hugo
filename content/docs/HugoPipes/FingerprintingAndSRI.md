+++
title = "Fingerprint"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Fingerprint

[https://gohugo.io/hugo-pipes/fingerprint/](https://gohugo.io/hugo-pipes/fingerprint/)

 	对给定的资源进行处理，添加资源内容的哈希字符串。  

## 语法

```
resources.Fingerprint RESOURCE [ALGORITHM]
fingerprint RESOURCE [ALGORITHM]
```

## 用法 

 	可以使用  `resources.Fingerprint`  对任何asset文件应用Fingerprinting和 [SRI](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)，该函数需要两个参数，分别为资源对象和一个可选的 [哈希算法](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms)。 

​	默认哈希算法为  `sha256` ，其他可用算法为  `sha384` ， `sha512` （自 Hugo  `0.55`  起），以及  `md5` 。  

​	经过处理的任何asset文件都将带有一个 `.Data.Integrity`  属性，其中包含由哈希算法名称、一个连字号（hyphen ）和 base64 编码的哈希值组成的完整性字符串。

```go-html-template
{{ $js := resources.Get "js/global.js" }}
{{ $secureJS := $js | resources.Fingerprint "sha512" }}
<script src="{{ $secureJS.Permalink }}" integrity="{{ $secureJS.Data.Integrity }}"></script>
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [FromString](https://gohugo.io/hugo-pipes/resource-from-string/)
- [Minify](https://gohugo.io/hugo-pipes/minification/)
