+++
title = "目录"
weight = 19
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Table of Contents - 目录

https://gohugo.io/content-management/toc/

​	Hugo可以自动解析Markdown内容并创建一个目录，您可以在模板中使用它。 

​	以前，没有开箱即用的方法来指定要渲染TOC的标题级别。[请参见相关的GitHub讨论(#1778)](https://github.com/gohugoio/hugo/issues/1778)。因此，从`{{ .Content }}`中提取时，生成的`<nav id="TableOfContents"><ul></ul></nav>`将从`<h1>`开始。

​	Hugo [v0.60.0](https://github.com/gohugoio/hugo/releases/tag/v0.60.0)切换到了[Goldmark](https://github.com/yuin/goldmark/)作为Markdown的默认库，该库具有改进和可配置的TOC实现。请看[如何为Goldmark渲染器配置TOC](https://gohugo.io/getting-started/configuration-markup/#table-of-contents)。

## 用法

​	以通常的标题方式创建您的Markdown。以下是一些示例内容：

```md
<!-- Your 前置元数据 up here -->

## Introduction

One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed into a horrible vermin.

## My Heading

He lay on his armour-like back, and if he lifted his head a little he could see his brown belly, slightly domed and divided by arches into stiff sections. The bedding was hardly able to cover it and seemed ready to slide off any moment.

### My Subheading

A collection of textile samples lay spread out on the table - Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of an illustrated magazine and housed in a nice, gilded frame. It showed a lady fitted out with a fur hat and fur boa who sat upright, raising a heavy fur muff that covered the whole of her lower arm towards the viewer. Gregor then turned to look out the window at the dull weather. Drops
```

​	Hugo将从`##Introduction`、`##My Heading`和`###My Subheading`创建一个目录，然后将其存储在[页面变量](https://gohugo.io/variables/page/)`.TableOfContents`中。

​	内置的`.TableOfContents`变量输出一个带有子`<ul>`元素的`<nav id="TableOfContents">`，其子`<li>`元素以适当的HTML标题开头。请查看[可用设置](https://gohugo.io/getting-started/configuration-markup/#table-of-contents)，以配置要在TOC中包含哪些标题级别。

## 模板示例：基本TOC 

​	以下是一个非常基本的[单页面模板](https://gohugo.io/templates/single-page-templates/)示例：

layout/_default/single.html

```go-html-template
{{ define "main" }}
<main>
    <article>
    <header>
        <h1>{{ .Title }}</h1>
    </header>
        {{ .Content }}
    </article>
    <aside>
        {{ .TableOfContents }}
    </aside>
</main>
{{ end }}
```

## 模板示例：TOC Partial 

​	以下是一个[部分模板](https://gohugo.io/templates/partials/)，它为页面级别控制目录添加了稍微更多的逻辑。它假定您在内容的前置元数据中使用`toc`字段，除非将其特别设置为`false`，否则会将TOC添加到具有大于400的`.WordCount`（请参见[页面变量](https://gohugo.io/variables/page/)）的任何页面。此示例还演示了如何在模板中使用[条件语句](https://gohugo.io/templates/introduction/#conditionals)：

layouts/partials/toc.html

```go-html-template
{{ if and (gt .WordCount 400 ) (.Params.toc) }}
<aside>
    <header>
    <h2>{{ .Title }}</h2>
    </header>
    {{ .TableOfContents }}
</aside>
{{ end }}
```

​	通过前面的示例，即使页面中有> 400个单词且`toc`未设置为`false`，如果页面中没有标题可以被`{{ .TableOfContents }}`变量提取，也不会渲染目录。

## 使用AsciiDoc 

​	Hugo支持使用AsciiDoc内容格式的目录。

​	在内容文件的头部，指定AsciiDoc TOC指令，以确保生成目录。Hugo将使用生成的TOC来填充页面变量`.TableOfContents`，方式与Markdown描述的相同。请参见以下示例：

```asciidoc
// <!-- Your 前置元数据 up here -->
:toc:
// Set toclevels to be at least your hugo [markup.tableOfContents.endLevel] config key
:toclevels: 4

== Introduction

One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed into a horrible vermin.

== My Heading

He lay on his armour-like back, and if he lifted his head a little he could see his brown belly, slightly domed and divided by arches into stiff sections. The bedding was hardly able to cover it and seemed ready to slide off any moment.

=== My Subheading

A collection of textile samples lay spread out on the table - Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of an illustrated magazine and housed in a nice, gilded frame. It showed a lady fitted out with a fur hat and fur boa who sat upright, raising a heavy fur muff that covered the whole of her lower arm towards the viewer. Gregor then turned to look out the window at the dull weather. Drops
```

​	Hugo将获取此AsciiDoc并创建目录，并将其存储在页面变量`.TableOfContents`中，与Markdown描述的相同。

## 另请参阅 

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
- [FromString](https://gohugo.io/hugo-pipes/resource-from-string/)
