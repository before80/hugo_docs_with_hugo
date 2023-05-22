+++
title = "简码变量"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Shortcode Variables- 简码变量

[https://gohugo.io/variables/shortcodes/](https://gohugo.io/variables/shortcodes/)

​	简码可以访问页面变量，并且有其自己的特定内置变量。 

​	[简码](https://gohugo.io/templates/shortcode-templates/)通过[`.Get`](https://gohugo.io/functions/get/)访问简码声明中分隔的参数、页面级别和站点级别的变量，还可以访问以下简码特定字段：

### .Name

​	简码名称。

### .Ordinal

​	与其父简码相对位置的零基序数。如果父简码是页面本身，则该序数将表示页面内容中此简码的位置。

### .Page

​	The owning ´Page`.

​	拥有此简码的页面。

### .Parent

​	为嵌套简码提供访问父简码上下文的能力。这对于从根继承常见简码参数非常有用。

### .Position

​	Contains [filename and position](https://godoc.org/github.com/gohugoio/hugo/common/text#Position) for the shortcode in a page. Note that this can be relatively expensive to calculate, and is meant for error reporting. See [Error Handling in Shortcodes](https://gohugo.io/templates/shortcode-templates/#error-handling-in-shortcodes).

​	包含页面中此简码的[文件名和位置](https://godoc.org/github.com/gohugoio/hugo/common/text#Position)。请注意，这可能是相对昂贵的计算，并且是用于错误报告的。请参见[简码错误处理](https://gohugo.io/templates/shortcode-templates/#error-handling-in-shortcodes)。

### .IsNamedParams

​	返回布尔值，当涉及的简码使用[命名参数而不是位置参数](https://gohugo.io/templates/shortcode-templates/)时返回`true`。

### .Inner

​	represents the content between the opening and closing shortcode tags when a [closing shortcode](https://gohugo.io/content-management/shortcodes/#shortcodes-with-markdown) is used

​	表示在使用[关闭简码](https://gohugo.io/content-management/shortcodes/#shortcodes-with-markdown)时开放和关闭简码标记之间的内容。

### .Scratch

​	返回一个可写的[`Scratch`](https://gohugo.io/functions/scratch)，以存储和操作将附加到此简码上下文的数据。此 Scratch 在服务器重新构建时会被重置。

### .InnerDeindent [New in v0.100.0](https://github.com/gohugoio/hugo/releases/tag/v0.100.0)

​	获取任何缩进已删除的`.Inner`。这是内置的`\{\{\< highlight \>\}\}`简码中使用的内容。

## 另请参阅

- [.Get](https://gohugo.io/functions/get/)
- [创建自己的简码](https://gohugo.io/templates/shortcode-templates/)
- [简码](https://gohugo.io/content-management/shortcodes/)
