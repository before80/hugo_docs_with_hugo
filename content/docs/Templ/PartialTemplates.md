+++
title = "局部模板"
weight = 13
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Partial Templates - 局部模板 

https://gohugo.io/templates/partials/

​	Partial 是在列表和页面模板中使用的更小的上下文感知组件，可以经济地使用以保持模板 DRY。

<iframe src="https://www.youtube.com/embed/pjS4pOLyB7c" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

## 局部模板查找顺序 

​	Partial 模板（如[单页面模板](https://gohugo.io/templates/single-page-templates/)和[列表页面模板](https://gohugo.io/templates/lists/)）具有特定的[查找顺序](https://gohugo.io/templates/lookup-order/)。然而，partial 更简单，因为 Hugo 只会检查两个地方：

1. `layouts/partials/*<PARTIALNAME>.html`
2. `themes/<THEME>/layouts/partials/*<PARTIALNAME>.html`

​	这允许某一主题的最终用户将 partial 的内容复制到同名文件中以进行[进一步的自定义](https://gohugo.io/hugo-modules/theme-components/)。

## 在您的模板中使用 Partial 

​	Hugo 项目中的所有 partial 都位于一个名为 `layouts/partials` 的目录中。为了更好的组织，您还可以在 `partials` 中创建多个子目录：

```txt
layouts/
└── partials/
    ├── footer/
    │   ├── scripts.html
    │   └── site-footer.html
    ├── head/
    │   ├── favicons.html
    │   ├── metadata.html
    │   ├── prerender.html
    │   └── twitter.html
    └── header/
        ├── site-header.html
        └── site-nav.html
```

​	在模板中调用所有 partial 都使用以下模式：

```go-html-template
{{ partial "<PATH>/<PARTIAL>.html" . }}
```

​	新手 Hugo 用户最常见的错误之一是未能向 partial 调用传递上下文。在上述模式中，请注意如何使用“点号”(`.`)作为第二个参数来给出 partial 上下文。您可以在[Hugo 模板介绍](https://gohugo.io/templates/introduction/)中了解更多有关"the dot"的信息。

​	`<PARTIAL>`包括`baseof`已被保留。（[#5373](https://github.com/gohugoio/hugo/issues/5373)）

​	如上例目录结构所示，您可以在`partials`中嵌套目录以获得更好的源代码组织。您只需要使用相对于`partials`目录的嵌套 partial 路径即可：

```go-html-template
{{ partial "header/site-header.html" . }}
{{ partial "footer/scripts.html" . }}
```

### 变量作用域 

​	partial 调用中的第二个参数是要传递下去的变量。上述示例传递了`.`，这告诉接收 partial 的模板应用当前[上下文](https://gohugo.io/templates/introduction/)。

​	这意味着 partial 只能访问这些变量。partial 是被隔离的，*无法访问外部作用域*。在 partial 内部，`$.Var` 等同于 `.Var`。

## 从 Partial 返回一个值 

​	除了输出标记之外，partial 还可以用于返回任何类型的值。为了返回一个值，partial 必须在*partial 的末尾*包括一个孤立的 `return` 语句。

### 示例 GetFeatured

```go-html-template
{{/* layouts/partials/GetFeatured.html */}}
{{ return first . (where site.RegularPages "Params.featured" true) }}
{{/* layouts/index.html */}}
{{ range partial "GetFeatured.html" 5 }}
  [...]
{{ end }}
```

### 示例 GetImage 

```go-html-template
{{/* layouts/partials/GetImage.html */}}
{{ $image := false }}
{{ with .Params.gallery }}
  {{ $image = index . 0 }}
{{ end }}
{{ with .Params.image }}
  {{ $image = . }}
{{ end }}
{{ return $image }}
{{/* layouts/_default/single.html */}}
{{ with partial "GetImage.html" . }}
  [...]
{{ end }}
```

​	每个 partial 文件只允许一个 `return` 语句。

## 内联 Partial 

​	您还可以在模板中内联定义 partial。但是请记住，模板命名空间是全局的，因此您需要确保名称是唯一的，以避免冲突。

```go-html-template
Value: {{ partial "my-inline-partial.html" . }}

{{ define "partials/my-inline-partial.html" }}
{{ $value := 32 }}
{{ return $value }}
{{ end }}
```

## 缓存的 Partials 

​	[`partialCached`模板函数](https://gohugo.io/functions/partialcached/)可以为不需要在每次调用时重新渲染的复杂模板提供显著的性能提升。最简单的用法如下：

```go-html-template
{{ partialCached "footer.html" . }}
```

​	您也可以传递附加参数给`partialCached`，以创建缓存 partial 模板的*变体*。

​	例如，您可以告诉Hugo只对每个章节渲染一次`footer.html` partial 模板：

```go-html-template
{{ partialCached "footer.html" . .Section }}
```

​	如果您需要传递额外的参数以创建唯一的变体，您可以传递任意数量的变体参数：

```go-html-template
{{ partialCached "footer.html" . .Params.country .Params.province }}
```

​	注意，变体参数不会被传递给底层的 partial 模板，它们只用于创建唯一的缓存键。

### 示例 `header.html` 

​	下面的`header.html` partial 模板被用于[spf13.com](https://spf13.com/)：

layouts/partials/header.html

```go-html-template
<!DOCTYPE html>
<html class="no-js" lang="en-US" prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb#">
<head>
    <meta charset="utf-8">

    {{ partial "meta.html" . }}

    <base href="{{ .Site.BaseURL }}">
    <title> {{ .Title }} : spf13.com </title>
    <link rel="canonical" href="{{ .Permalink }}">
    {{ if .RSSLink }}<link href="{{ .RSSLink }}" rel="alternate" type="application/rss+xml" title="{{ .Title }}" />{{ end }}

    {{ partial "head_includes.html" . }}
</head>
```

​	`header.html` 这个示例的partial 是在 Hugo 引入 block templates 之前创建的。关于如何定义主模板（例如站点的头部、页头和页脚）的外部 chrome 或 shell，可以在 [base templates and blocks](https://gohugo.io/templates/base/) 中了解更多信息。您甚至可以组合使用 blocks 和 partials，以增加灵活性。

### 示例 `footer.html` 

​	下面的`footer.html` partial 模板被用于[spf13.com](https://spf13.com/)：

layouts/partials/footer.html

```go-html-template
<footer>
  <div>
    <p>
    &copy; 2013-14 Steve Francia.
    <a href="https://creativecommons.org/licenses/by/3.0/" title="Creative Commons Attribution">Some rights reserved</a>;
    please attribute properly and link back.
    </p>
  </div>
</footer>
```

## 另请参阅

- [.GetPage](https://gohugo.io/functions/getpage/)
- [内容z章节](https://gohugo.io/content-management/sections/)
- [内容类型 ](https://gohugo.io/content-management/types/)
- [在 Hugo 中的内容列表 ](https://gohugo.io/templates/lists/)
- [菜单模板](https://gohugo.io/templates/menu-templates/)
