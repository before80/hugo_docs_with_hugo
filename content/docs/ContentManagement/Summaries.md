+++
title = "内容摘要"
weight = 14
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Content Summaries - 内容摘要 

[https://gohugo.io/content-management/summaries/](https://gohugo.io/content-management/summaries/)

​	Hugo 可以生成内容的摘要。 

​	通过使用`.Summary`[页面变量](https://gohugo.io/variables/page/)，Hugo会生成内容摘要以在摘要视图中用作简短版本。

## 摘要拆分选项 

- 自动摘要拆分 
- 手动摘要拆分 
- 前置元数据摘要

​	在摘要中附带指向原始内容的链接是很自然的，常见的设计模式是以"Read More …"按钮的形式渲染。参见 `.RelPermalink`、`.Permalink` 和 `.Truncated` [页面变量](https://gohugo.io/variables/page/)。

### 自动摘要拆分 

​	默认情况下，Hugo 会自动将内容的前 70 个字作为摘要，并将其存储在 `.Summary` 页面变量中供模板使用。您可以通过在[站点配置](https://gohugo.io/getting-started/configuration/)中设置 `summaryLength` 来自定义摘要长度。

> ​	您可以使用 `plainify` 和 `safeHTML` 等函数自定义摘要中加载的 HTML 标记的方式。

> ​	Hugo 定义的摘要使用的是通过将文本按一个或多个连续空格字符拆分计算的字数。如果您使用 `CJK` 语言创建内容，并希望使用 Hugo 的自动摘要拆分，请在[站点配置](https://gohugo.io/getting-started/configuration/)中将 `hasCJKLanguage` 设置为 `true`。

### 手动摘要拆分 

​	或者，您可以在想要拆分文章的地方添加 `<!--more-->` 摘要分隔符。

​	对于 [Org 模式内容](https://gohugo.io/content-management/formats/)，请在想要拆分文章的地方使用 `# more`。

​	摘要分隔符之前的内容将用作该内容的摘要，并以完整的 HTML 格式存储在 `.Summary` 页面变量中。

> ​	摘要分隔符的概念不仅仅适用于 Hugo。在其他文献中，它也被称为"more tag"或"excerpt separator"。

- Pros（优点）

  自由、精度和提高渲染质量。所有 HTML 标记和格式都会被保留。 

- Cons（缺点）

  需要内容作者额外的工作，因为他们需要记得在每个内容文件中输入 `<!--more-->`（或 [org 内容](https://gohugo.io/content-management/formats/)为 `# more`）。可以通过在`原型`的前置元数据下方添加摘要分隔符来自动化这一过程。 

​	请确保精确输入 `<!--more-->`；即全部小写且没有空格。

### 前置元数据摘要

​	您可能希望文章摘要不是从文章开头开始的文本。在这种情况下，您可以在文章前置元数据的`summary`变量中提供一个单独的摘要。

- Pros（优点）

  完全自由的文本，与文章内容无关。可以在摘要中使用标记。 

- Cons（缺点）

  对于内容作者来说，需要编写一个完全独立的文本作为文章的摘要，这会增加额外的工作量。 

## 摘要选择顺序 

​	因为有多种方法可以指定摘要，了解 Hugo 在决定返回 `.Summary` 的文本时遵循的选择顺序是有用的。它如下所示：

1. 如果文章中存在 `<!--more-->` 摘要分隔符，则提供分隔符之前的文本，按照手动摘要拆分方法。 
2. 如果文章前置元数据中有一个`summary`变量，则按照前置元数据摘要方法提供变量的值。  
3. 按照自动摘要拆分方法，提供文章开头的文本。 

> ​	Hugo 使用上述步骤中返回的第一个文本。因此，例如，如果您的文章在其前言中具有`summary`变量和一个 `<!--more-->` 摘要分隔符，Hugo 将使用手动摘要拆分方法。

## 示例：前 10 篇带摘要的文章 

​	您可以使用以下代码显示内容摘要。例如，您可以在一个[章节模板](https://gohugo.io/templates/section-templates/)中使用以下代码片段。

page-list-with-summaries.html

```go-html-template
{{ range first 10 .Pages }}
    <article>
      <!-- this <div> includes the title summary -->
      <div>
        <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
        {{ .Summary }}
      </div>
      {{ if .Truncated }}
      <!-- This <div> includes a read more link, but only if the summary is truncated... -->
      <div>
        <a href="{{ .RelPermalink }}">Read More…</a>
      </div>
      {{ end }}
    </article>
{{ end }}
```

注意，当内容未被截断时，即摘要包含整篇文章时，`.Truncated` 布尔变量值可以用于隐藏"Read More…"链接。
