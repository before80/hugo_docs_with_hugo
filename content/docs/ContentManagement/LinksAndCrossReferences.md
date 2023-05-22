+++
title = "链接和交叉引用"
weight = 15
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Links and Cross References - 链接和交叉引用 

[https://gohugo.io/content-management/cross-references/](https://gohugo.io/content-management/cross-references/)

​	用于创建指向文档的简码链接。 

​	`ref`和`relref`简码分别显示文档的绝对和相对永久链接。

## 使用`ref`和`relref` 

​	`ref`和`relref`简码需要一个参数：指向内容文档的路径，带有或不带有文件扩展名，带有或不带有锚点。没有前导 `/` 的路径首先相对于当前页面解析，然后相对于站点的其余部分解析。

```
.
└── content
    ├── about
    |   ├── _index.md
    |   └── credits.md
    ├── pages
    |   ├── document1.md
    |   └── document2.md    // has anchor #anchor
    ├── products
    |   └── index.md
    └── blog
        └── my-post.md
```

​	这些页面可以按以下方式被引用：

```text
\{\{\< ref "document2" \>\}\}             // <- From pages/document1.md, relative path
\{\{\< ref "document2#anchor" \>\}\}      
\{\{\< ref "document2.md" \>\}\}          
\{\{\< ref "document2.md#anchor" \>\}\}   
\{\{\< ref "#anchor" \>\}\}               // <- From pages/document2.md
\{\{\< ref "/blog/my-post" \>\}\}         // <- From anywhere, absolute path
\{\{\< ref "/blog/my-post.md" \>\}\}
\{\{\< relref "document" \>\}\}
\{\{\< relref "document.md" \>\}\}
\{\{\< relref "#anchor" \>\}\}
\{\{\< relref "/blog/my-post.md" \>\}\}
```

​	`index.md`可以被其路径或其不带结尾 `/` 的所在文件夹引用。`_index.md`只被其所在文件夹引用：

```text
\{\{\< ref "/about" \>\}\}             // <- References /about/_index.md
\{\{\< ref "/about/_index" \>\}\}      //    Raises REF_NOT_FOUND error
\{\{\< ref "/about/credits.md" \>\}\}  // <- References /about/credits.md

\{\{\< ref "/products" \>\}\}          // <- References /products/index.md
\{\{\< ref "/products/index" \>\}\}    // <- References /products/index.md
```

​	在Markdown中使用`ref`或`relref`生成超链接：

```text
[About](\{\{\< ref "/about" \>\}\} "About Us")
```

​	如果文档无法被唯一解析，Hugo将发出错误或警告。错误行为可配置，请参阅下文。

### 链接到另一种语言版本 

​	要链接到文档的另一种语言版本，请使用以下语法：

```go-html-template
\{\{\< relref path="document.md" lang="ja" \>\}\}
```

### 获取另一种输出格式 

​	要链接到文档的另一种输出格式，请使用以下语法：

```go-html-template
\{\{\< relref path="document.md" outputFormat="rss" \>\}\}
```

### 标题ID 

​	使用Markdown文档类型时，Hugo为页面上的每个标题生成元素ID。例如：

```md
## Reference
```

生成以下HTML：

```html
<h2 id="reference">Reference</h2>
```

​	在使用`ref`或`relref`简码时，通过将ID附加到路径来获取标题的永久链接：

```go-html-template
\{\{\< ref "document.md#reference" \>\}\}
\{\{\< relref "document.md#reference" \>\}\}
```

​	通过包含属性来生成自定义标题ID。例如：

```md
## Reference A {#foo}
## Reference B {id="bar"}
```

生成以下HTML：

```html
<h2 id="foo">Reference A</h2>
<h2 id="bar">Reference B</h2>
```

​	如果同一标题在页面上出现多次，Hugo将生成唯一的元素ID。例如：

```md
## Reference
## Reference
## Reference
```

生成以下HTML：

```html
<h2 id="reference">Reference</h2>
<h2 id="reference-1">Reference</h2>
<h2 id="reference-2">Reference</h2>
```

## Ref 和 RelRef 配置 

​	自 Hugo 0.45 开始，该行为可以在 `config.toml` 中进行配置：

- refLinksErrorLevel ("ERROR")

  使用`ref`或`relref`解析页面链接时，如果链接无法解析，将使用此日志级别记录。有效值为`ERROR`（默认）或`WARNING`。任何`ERROR`都将导致构建失败（`exit -1`）。 

- refLinksNotFoundURL

  在 `ref` 或 `relref` 中找不到页面引用时使用的 URL 占位符。则原样使用。 
  
  

## 另请参阅 

- [ref](https://gohugo.io/functions/ref/)
- [relref](https://gohugo.io/functions/relref/)
- [URL 管理 ](https://gohugo.io/content-management/urls/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [absURL](https://gohugo.io/functions/absurl/)
