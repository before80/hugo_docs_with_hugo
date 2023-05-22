+++
title = "目录结构"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Directory Structure - 目录结构 

[https://gohugo.io/getting-started/directory-structure/](https://gohugo.io/getting-started/directory-structure/)

​	Hugo的CLI脚手架会创建一个项目目录结构，然后使用该单个目录作为输入来创建一个完整的站点。 

## 新建站点脚手架

<iframe src="https://www.youtube.com/embed/sB0HLHjgQ7E" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 544px; height: 306px; border: 0px;"></iframe>

​	从命令行运行`hugo new site example`会创建一个带有以下元素的目录结构：

```txt
example/
├── archetypes/
│   └── default.md
├── assets/
├── content/
├── data/
├── layouts/
├── public/
├── static/
├── themes/
└── config.toml
```

## 目录结构说明 

​	以下是每个目录的高级概述，并提供了链接到Hugo文档中各自部分的链接。

- [archetypes](https://gohugo.io/content-management/archetypes/)

  您可以使用`hugo new`命令在Hugo中创建新的内容文件。默认情况下，Hugo将创建带有`date`、`title`（从文件名推断）和`draft = true`的新内容文件。这节省了时间，并为使用多个内容类型的站点促进了一致性。您还可以创建自己的原型（[archetypes](https://gohugo.io/content-management/archetypes/)），其中包含自定义的预配置前置元数据字段。 

- [assets](https://gohugo.io/hugo-pipes/introduction#asset-directory)

  存储需要由[Hugo Pipes](https://gohugo.io/hugo-pipes/)处理的所有文件。只有使用`.Permalink`或`.RelPermalink`的文件将被发布到`public`目录。 

- [`config`](https://gohugo.io/getting-started/configuration/)

  Hugo带有大量的[配置指令](https://gohugo.io/getting-started/configuration/#all-configuration-settings)。[config目录](https://gohugo.io/getting-started/configuration/#configuration-directory)是存储这些指令的地方，以JSON、YAML或TOML文件的形式存储。每个根设置对象都可以作为自己的文件，并按环境结构化。设置最少且不需要环境感知的项目可以在其根目录使用单个`config.toml`文件。
  
  许多站点可能不需要任何配置，但Hugo提供了大量的[配置指令](https://gohugo.io/getting-started/configuration/#all-configuration-settings)，用于更精细的指导如何构建您的站点。注意：config目录不会默认创建。



- [`content`](https://gohugo.io/content-management/organization/)

  您站点的所有内容都将位于此目录中。Hugo中的每个顶层文件夹都被视为[内容章节](https://gohugo.io/content-management/sections/)。例如，如果您的站点有三个主要章节——博客（blog）、文章（articles）和教程（tutorials）——则在`content/blog`、`content/articles`和`content/tutorials`中将会有三个目录。Hugo使用章节来分配默认[内容类型](https://gohugo.io/content-management/types/)。

- [`data`](https://gohugo.io/templates/data-templates/)

  此目录用于存储在生成站点时Hugo可以使用的配置文件。您可以按YAML、JSON或TOML格式编写这些文件。除了将这些文件添加到此文件夹中外，您还可以创建从动态内容中提取的[数据模板](https://gohugo.io/templates/data-templates/)。

- [`layouts`](https://gohugo.io/templates/)

  存储模板，以`.html`文件的形式指定如何将您的内容视图渲染为静态站点。模板包括[列表页面](https://gohugo.io/templates/lists/)、[主页](https://gohugo.io/templates/homepage/)、[分类法模板](https://gohugo.io/templates/taxonomy-templates/)、[局部](https://gohugo.io/templates/partials/)、[单页模板](https://gohugo.io/templates/single-page-templates/)等。

- [`static`](https://gohugo.io/content-management/static-files/)

  存储所有的静态内容：图片、CSS、JavaScript等。当Hugo构建您的站点时，static目录内的所有资源都将按原样复制。一个使用`static`目录的好例子是[在Google Search Console上验证站点所有权](https://support.google.com/webmasters/answer/9008080#zippy=%2Chtml-file-upload)，您希望Hugo复制完整的HTML文件而不修改其内容。 

​	从 **Hugo 0.31** 版本开始，您可以有多个静态目录。

- [resources](https://gohugo.io/getting-started/configuration/#configure-file-caches)

  缓存一些文件以加速生成。也可以由模板作者用于分发已构建的 Sass 文件，这样您就不必安装预处理器。注意：默认情况下不会创建`resources` 目录。 

## 另请参阅 

- [配置模块](https://gohugo.io/hugo-modules/configuration/) 
- [主题组件](https://gohugo.io/hugo-modules/theme-components/) 
- [使用 Hugo 模块](https://gohugo.io/hugo-modules/use-modules/) 
- [静态文件](https://gohugo.io/content-management/static-files/) 
- [评论](https://gohugo.io/content-management/comments/)
