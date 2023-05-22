+++
title = "主页模板"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Homepage Template - 主页模板 

[https://gohugo.io/templates/homepage/](https://gohugo.io/templates/homepage/)

​	站点的主页通常与其他页面格式不同。因此，Hugo 使您能够轻松地将新站点的主页定义为独特的模板。 

​	主页是一个`Page`，因此可使用所有[页面变量](https://gohugo.io/variables/page/)和[站点变量](https://gohugo.io/variables/site/)。

​	主页模板是构建站点所必需的唯一模板，因此在启动新站点和模板时非常有用。如果您正在开发单页面站点，则它也是唯一必需的模板。

<iframe src="https://www.youtube.com/embed/ut1xtRZ1QOA" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

## 主页模板查找顺序 

​	请参见[模板查找](https://gohugo.io/templates/lookup-order/)。

## 向主页添加内容和前置元数据 

​	主页与 [Hugo 中的其他列表页](https://gohugo.io/templates/lists/)面类似，可以从 `_index.md` 文件接受内容和 前置元数据。该文件应该位于您的 `content` 文件夹的根目录下（即 `content/_index.md`）。然后，您可以像处理其他任何内容文件一样向主页添加正文和元数据（metadata ）。

​	有关如何使用 `_index.md` 向列表页面添加内容和前置元数据的更多信息，请参见下面的主页模板或[内容组织](https://gohugo.io/content-management/organization/)。

## 示例主页模板 

​	以下是一个主页模板示例，它使用 [partial](https://gohugo.io/templates/partials/)、[基础](https://gohugo.io/templates/base/)模板和位于 `content/_index.md` 中的内容文件来填充 `{{ .Title }}` 和 `{{ .Content }}` [页面变量](https://gohugo.io/variables/page/)。

layouts/index.html

```go-html-template
{{ define "main" }}
  <main aria-role="main">
    <header class="homepage-header">
      <h1>{{ .Title }}</h1>
      {{ with .Params.subtitle }}
      <span class="subtitle">{{ . }}</span>
      {{ end }}
    </header>
    <div class="homepage-content">
      <!-- Note that the content for index.html, as a sort of list page, will pull from content/_index.md -->
      {{ .Content }}
    </div>
    <div>
      {{ range first 10 .Site.RegularPages }}
          {{ .Render "summary" }}
      {{ end }}
    </div>
  </main>
{{ end }}
```
