+++
title = "Hugo Pipes 简介"
weight = 1
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Hugo Pipes Introduction - Hugo Pipes 简介

[https://gohugo.io/hugo-pipes/introduction/](https://gohugo.io/hugo-pipes/introduction/)

​	Hugo Pipes 是 Hugo 的asset 处理函数集合。

## 在 /assets 中查找资源

​	这是关于全局资源（global Resources），它们在 `/assets` 内部挂载。有关 `.Page` 作用域内的资源，请参见 [Page Resources](https://gohugo.io/content-management/page-resources/)。

​	请注意，您可以使用 [Mount Configuration](https://gohugo.io/hugo-modules/configuration/#module-config-mounts) 将任何目录挂载到 Hugo 的虚拟 `assets` 文件夹中。

| 函数                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| `resources.Get`       | Get 会查找在 Hugo assets 文件系统中给定的文件名，并创建一个可用于进一步转换的 `Resource` 对象。请参见 [使用 resources.Get 和 resources.GetRemote 获取资源](https://gohugo.io/hugo-pipes/introduction/#get-resource-with-resourcesget-and-resourcesgetremote)。 |
| `resources.GetRemote` | 与 `Get` 相同，但它接受远程 URL。请参见 [使用 resources.Get 和 resources.GetRemote 获取资源](https://gohugo.io/hugo-pipes/introduction/#get-resource-with-resourcesget-and-resourcesgetremote)。 |
| `resources.GetMatch`  | `GetMatch` 查找第一个与给定模式匹配的资源，如果没有找到，则返回 `nil`。有关使用的规则的更完整解释，请参见 Match。 |
| `resources.Match`     | `Match` 获取与给定基本路径前缀匹配的所有资源，例如 "*.png" 将匹配所有 png 文件。 "*" 不匹配路径分隔符 (/)，因此，如果您将资源组织在子文件夹中，则需要明确指定，例如："images/*.png"。要匹配包中任何 PNG 图像，您可以使用 "**.png"，要匹配 images 文件夹下所有 PNG 图像，请使用 "images/**.jpg"。匹配区分大小写。Match 通过使用相对于文件系统根的路径的文件名来匹配，路径使用 Unix 样式斜杠 (/)，没有前导斜杠，例如 "images/logo.png"。有关完整规则集，请参见 [https://github.com/gobwas/glob](https://github.com/gobwas/glob)。 |

​	有关此命名空间中所有模板函数的最新概述，请参见 [GoDoc Page](https://pkg.go.dev/github.com/gohugoio/hugo@v0.93.1/tpl/resources)。

## 使用 resources.Get 和 resources.GetRemote 获取资源

​	为了使用 Hugo Pipes 处理资源，必须使用 `resources.Get` 或 `resources.GetRemote` 获取它作为一个 `Resource`。

​	对于 `resources.Get`，第一个参数是相对于 `assets` 目录/目录的本地路径：

```go-html-template
{{ $local := resources.Get "sass/main.scss" }}
```

​	对于 `resources.GetRemote`，第一个参数是远程 URL：

```go-html-template
{{ $remote := resources.GetRemote "https://www.example.com/styles.scss" }}
```

`resources.Get` and `resources.GetRemote` return `nil` if the resource is not found.

​	`resources.Get` 和 `resources.GetRemote` 如果找不到资源则返回 `nil`。

[新版本v0.110.0](https://github.com/gohugoio/hugo/releases/tag/v0.110.0)您可以使用返回的 `Resource` 中的 `.Data` 获取有关HTTP响应的信息。这对于没有任何正文的HEAD请求特别有用。数据对象包含：  

- StatusCode

  HTTP状态代码，例如200状态  

  HTTP状态文本，例如"200 OK" TransferEncoding

  传输编码，例如"chunked" ContentLength

  内容长度，例如1234 ContentType

  内容类型，例如"text/html"

### 缓存 

​	默认情况下，Hugo基于给定的 `URL` 和 `options` (例如，标题)计算缓存键。  

[新版本v0.97.0](https://github.com/gohugoio/hugo/releases/tag/v0.97.0)您可以通过在选项映射中设置 `key` 来覆盖此设置。这可用于更精细地控制远程资源的获取频率，例如：

```go-html-template
{{ $cacheKey := print $url (now.Format "2006-01-02") }}
{{ $resource := resource.GetRemote $url (dict "key" $cacheKey) }}
```

### 错误处理 

​	从 `resources.GetRemote` 返回的返回值包括一个 `.Err` 方法，如果调用失败，则会返回错误。如果您只想将任何错误记录为 `WARNING` ，则可以使用类似于下面的结构。

```go-html-template
{{ with resources.GetRemote "https://gohugo.io/images/gohugoio-card-1.png" }}
  {{ with .Err }}
    {{ warnf "%s" . }}
  {{ else }}
    <img src="{{ .RelPermalink }}" width="{{ .Width }}" height="{{ .Height }}" alt="">
  {{ end }}
{{ end }}
```

​	请注意，如果您不自己处理 `.Err` ，Hugo将在您开始使用 `Resource` 对象的第一次构建时失败。  

### 远程选项 

​	在获取远程 `Resource` 时， `resources.GetRemote` 接收一个可选的选项映射作为第二个参数，例如：

```go-html-template
{{ $resource := resources.GetRemote "https://example.org/api" (dict "headers" (dict "Authorization" "Bearer abcd")) }}
```

​	如果您需要同一头键的多个值，请使用切片：

```go-html-template
{{ $resource := resources.GetRemote "https://example.org/api"  (dict "headers" (dict "X-List" (slice "a" "b" "c"))) }}
```

​	您还可以更改请求方法并设置请求正文：

```go-html-template
{{ $postResponse := resources.GetRemote "https://example.org/api"  (dict 
    "method" "post"
    "body" `{"complete": true}` 
    "headers" (dict 
        "Content-Type" "application/json"
    )
)}}
```

### 远程资源的缓存

​	使用 `resources.GetRemote` 获取的远程资源将缓存在磁盘上。有关详情，请参见[配置文件缓存](https://gohugo.io/getting-started/configuration/#configure-file-caches)。 

## 复制资源

[New in v0.100.0](https://github.com/gohugoio/hugo/releases/tag/v0.100.0)

 `resources.Copy` 使您可以复制几乎任何Hugo `Resource`（唯一的例外是`Page`），可能最有用的是重命名：

```go-html-template
{{ $resized := $image.Resize "400x400" |  resources.Copy "images/mynewname.jpg" }}
<img src="{{ $resized.RelPermalink }}">
```

## Asset 目录 

​	asset 文件必须存储在asset 目录中。默认为 `/assets` ，但可以通过配置文件的 `assetDir` 键进行配置。  

### Asset 发布  

​	当您调用 `.Permalink` ， `.RelPermalink` 或 `.Publish` 时，Hugo将assets 发布到 `publishDir` （通常为 `public` ）。您可以使用 `.Content` 来内联assets 。  

## Go 管道 

​	为了提高可读性，本文档的Hugo Pipes示例将使用[Go Pipes](https://gohugo.io/templates/introduction/#pipes)编写：

```go-html-template
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS | resources.Minify | resources.Fingerprint }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```

## 方法别名

​	每个 Hugo Pipes 的 `resources` 转换方法都使用 **驼峰式** 别名（例如 `resources.ToCSS` 的别名是 `toCSS`）。没有这样别名的非转换方法包括 `resources.Get`、`resources.FromString`、`resources.ExecuteAsTemplate` 和 `resources.Concat`。

​	因此，上面的示例也可以写成以下形式：

```go-html-template
{{ $style := resources.Get "sass/main.scss" | toCSS | minify | fingerprint }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```

## 缓存  

​	Hugo 管道调用基于整个*管道链*进行缓存。  

​	一个管道链的示例是：

```go-html-template
{{ $mainJs := resources.Get "js/main.js" | js.Build "main.js" | minify | fingerprint }}
```

​	管道链仅在站点构建中第一次遇到时调用，否则结果将从缓存中加载。因此，Hugo 管道可以在执行数千或数百万次的模板中使用，而不会对构建性能产生负面影响。
