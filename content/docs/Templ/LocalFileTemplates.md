+++
title = "本地文件模板"
weight = 15
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Local File Templates - 本地文件模板 

[https://gohugo.io/templates/files/](https://gohugo.io/templates/files/)

​	Hugo 的 `readDir` 和 `readFile` 函数使得遍历项目目录结构和将文件内容写入模板变得容易。

## 遍历本地文件 

​	使用 Hugo 的 [readDir](https://gohugo.io/functions/readdir/) 和 [readFile](https://gohugo.io/functions/readfile/) 模板函数，您可以遍历服务器上站点的文件。

## 使用 `readDir` 

​	[`readDir` 函数](https://gohugo.io/functions/readdir/) 返回一个由 [`os.FileInfo`](https://golang.org/pkg/os/#FileInfo) 组成的数组。它以文件的 `path` 作为单个字符串参数。这个路径可以指向您站点上的任何目录（即服务器文件系统中的目录）。

​	路径是绝对还是相对并不重要，因为对于 `readDir` 函数，您站点的根目录（通常是 `./public/`）实际上同时扮演两个角色：

1. 文件系统根目录 
3. 当前工作目录 

## 使用 `readFile` 

​	[`readfile` 函数](https://gohugo.io/functions/readfile/) 从磁盘读取文件并将其转换为字符串，以便由其他 Hugo 函数操纵或按原样添加。`readFile` 将文件（包括路径）作为传递给该函数的参数。

​	在模板中使用 `readFile` 函数时，请确保路径相对于*Hugo 项目根目录*：

```go-html-template
{{ readFile "/content/templates/local-file-templates" }}
```

### `readFile` 示例：将项目文件添加到内容 

​	由于 `readFile` 是一个函数，因此它仅在模板中可用，而不在内容中可用。然而，我们可以创建一个简单的 [简码模板](https://gohugo.io/templates/shortcode-templates/)，来调用 `readFile`，将第一个参数通过该函数传递，然后允许一个可选的第二个参数将文件通过 Markdown 处理器。将这个 简码添加到内容中的模式如下：

```go-html-template
\{\{\< readfile file="/path/to/local/file.txt" markdown="true" \>\}\}
```

​	如果要使用 `readFile` 为主题创建[自定义简码](https://gohugo.io/templates/shortcode-templates/)，请注意，简码的使用将参考项目根目录，而不是您的 `themes` 目录。

## 另请参阅

- [配置模块 ](https://gohugo.io/hugo-modules/configuration/)
- [目录结构 ](https://gohugo.io/getting-started/directory-structure/)
- [文件变量 ](https://gohugo.io/variables/files/)
- [静态文件 ](https://gohugo.io/content-management/static-files/)
- [主题组件](https://gohugo.io/hugo-modules/theme-components/)
