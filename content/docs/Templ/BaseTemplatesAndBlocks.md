+++
title = "基础模板和块"
weight = 4
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Base Templates and Blocks - 基础模板和块 

[https://gohugo.io/templates/base/](https://gohugo.io/templates/base/)

​	基本模板和块结构允许您定义主模板的外壳（即页面的Chrome）。 

​	`block`关键字允许您定义页面一个或多个主模板的外壳，然后根据需要填充或覆盖部分（portions ）。

<iframe src="https://www.youtube.com/embed/QVOMCYitLEc" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

## 基础模板查找顺序 

​	基础模板查找顺序紧跟它所应用的模板的查找顺序（例如，`_default/list.html`）。

​	有关详细信息和示例，请参见[模板查找顺序](https://gohugo.io/templates/lookup-order/)。

## 定义基础模板 

​	以下定义了一个简单的基础模板 `_default/baseof.html`。作为默认模板，它是从所有页面渲染的外壳，除非您在查找顺序的开头指定另一个`*baseof.html`。

layouts/_default/baseof.html

```go-html-template
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ block "title" . }}
      <!-- Blocks may include default content. -->
      {{ .Site.Title }}
    {{ end }}</title>
  </head>
  <body>
    <!-- Code that all your templates share, like a header -->
    {{ block "main" . }}
      <!-- The part of the page that begins to differ between templates -->
    {{ end }}
    {{ block "footer" . }}
    <!-- More shared code, perhaps a footer but that can be overridden if need be in  -->
    {{ end }}
  </body>
</html>
```

## 覆盖基础模板 

​	从上面的基本模板，您可以定义[默认的列表模板](https://gohugo.io/templates/lists)。默认的列表模板将继承上面定义的所有代码，然后可以根据需要实现自己的`"main"`块：

layouts/_default/list.html

```go-html-template
{{ define "main" }}
  <h1>Posts</h1>
  {{ range .Pages }}
    <article>
      <h2>{{ .Title }}</h2>
      {{ .Content }}
    </article>
  {{ end }}
{{ end }}
```

​	这将用实际有用的内容替换我们（基本上为空的）`"main"`块的内容，对于列表中的内容，我们没有定义`"title"`块，因此在列表中保留了来自基础模板的内容。

​	放置在块定义之外的代码会破坏您的布局，这甚至包括HTML注释。例如：

```go-html-template
<!-- Seemingly harmless HTML comment..that will break your layout at build -->
{{ define "main" }}
...your code here
{{ end }}
```

[请参见Hugo讨论论坛中的此主题](https://discourse.gohugo.io/t/baseof-html-block-templates-and-list-types-results-in-empty-pages/5612/6)。

​	以下显示了如何使用特定于[默认单个页面模板](https://gohugo.io/templates/single-page-templates/)的代码覆盖基础模板的`"main"`和`"title"`块区域：

layouts/_default/single.html

```go-html-template
{{ define "title" }}
  <!-- This will override the default value set in baseof.html; i.e., "{{ .Site.Title }}" in the original example-->
  {{ .Title }} &ndash; {{ .Site.Title }}
{{ end }}
{{ define "main" }}
  <h1>{{ .Title }}</h1>
  {{ .Content }}
{{ end }}
```

## 另请参阅  

- [path.Base](https://gohugo.io/functions/path.base/)
- [path.BaseName](https://gohugo.io/functions/path.basename/)
