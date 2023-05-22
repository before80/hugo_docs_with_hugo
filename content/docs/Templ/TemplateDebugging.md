+++
title = "模板调试"
weight = 26
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Template Debugging - 模板调试 

[https://gohugo.io/templates/template-debugging/](https://gohugo.io/templates/template-debugging/)

​	您可以使用 Go 模板的 `printf` 函数来调试 Hugo 模板。这些代码片段提供了一种快速简便的方式来可视化不同上下文中可用的变量。

​	以下是一些可以添加到您的模板中以回答一些常见问题的代码片段。

​	这些代码片段使用 Go 模板中的 `printf` 函数。这个函数是 Go 函数 [fmt.Printf](https://pkg.go.dev/fmt) 的别名。



## 此上下文中有哪些变量可用？ 

​	您可以使用模板语法 `$.` 来获取该模板的顶层上下文。这将打印出`.Site`下的所有值。

```go-html-template
{{ printf "%#v" $.Site }}
```

​	这将打印出`.Permalink`的值：

```go-html-template
{{ printf "%#v" .Permalink }}
```

​	这将打印出当前上下文（`.`，也称为"the dot"）的所有变量的列表。

```go-html-template
{{ printf "%#v" . }}
```

​	在开发 [homepage](https://gohugo.io/templates/homepage/) 时，您正在遍历的页面之一是什么样子的？

```go-html-template
{{ range .Pages }}
    {{/* The context, ".", is now each one of the pages as it goes through the loop */}}
    {{ printf "%#v" . }}
{{ end }}
```

## 为什么我没有显示定义的变量？ 

​	检查是否在 `partial` 函数中传递了变量：

```go-html-template
{{ partial "header.html" }}
```

​	这个例子将渲染 header partial，但 header partial 将没有访问任何上下文变量的权限。您需要显式地传递变量。例如，注意添加了 ["the dot"](https://gohugo.io/templates/introduction/)。

```go-html-template
{{ partial "header.html" . }}
```

​	点（`.`）被认为是理解 Hugo 模板的基础。更多信息，请参见 [Introduction to Hugo Templating](https://gohugo.io/templates/introduction/)。
