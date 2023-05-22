+++
title = "Default"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# default

[https://gohugo.io/functions/default/](https://gohugo.io/functions/default/)

​	`default`函数用于当第一个值未被设置时，返回可以被返回的默认值。

## 语法

```
default DEFAULT INPUT
```

​	`default`函数检查给定值是否被设置，如果没有被设置，则返回默认值。在此上下文中，“设置”意味着不同的事情，具体取决于数据类型： 

- 对于数字类型和时间类型，为非零值
- 对于字符串、数组、切片和映射，为非零长度
- 对于布尔或结构体值，为任何值
- 对于任何其他类型，为非nil值

​	`default`函数示例引用以下内容页面：

content/posts/default-function-example.md

```md
---
title: Sane Defaults
seo_title:
date: 2017-02-18
font:
oldparam: The default function helps make your templating DRYer.
newparam:
---
```

​	`default`可以以多种方式编写：

```go-html-template
{{ .Params.font | default "Roboto" }}
{{ default "Roboto" .Params.font }}
```

​	上述两个 `default`函数调用都返回`Roboto`。

​	但是，`default`值不需要像上面的例子一样被硬编码。`default`值可以是变量或直接使用点符号从前置元数据中提取：

```go-html-template
{{ $old := .Params.oldparam }}
<p>{{ .Params.newparam | default $old }}</p>
```

它将返回：

```html
<p>The default function helps make your templating DRYer.</p>
```

然后使用点符号：

```go-html-template
<title>{{ .Params.seo_title | default .Title }}</title>
```

它将返回：

```html
<title>Sane Defaults</title>
```

​	以下内容具有等效的返回值，但`default`更为简洁。这演示了`default`的实用性：

使用`if`:

```go-html-template
<title>{{ if .Params.seo_title }}{{ .Params.seo_title }}{{ else }}{{ .Title }}{{ end }}</title>
=> Sane Defaults
```

使用`with`:

```go-html-template
<title>{{ with .Params.seo_title }}{{ . }}{{ else }}{{ .Title }}{{ end }}</title>
=> Sane Defaults
```
