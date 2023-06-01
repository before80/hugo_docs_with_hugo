+++
title = ".Get"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Get

[https://gohugo.io/functions/get/](https://gohugo.io/functions/get/)

​	访问简码声明中的位置参数和有序参数。

## 语法

```
.Get INDEX
.Get KEY
```

​	`.Get` 是在创建您自己的 [简码模板](https://gohugo.io/templates/shortcode-templates/) 时专门用于访问传递给它的 [位置和命名](https://gohugo.io/templates/shortcode-templates/#positional-vs-named-parameters) 参数。当与数字索引一起使用时，它查询位置参数（从 0 开始）。使用字符串键时，它查询命名参数。 

​	当访问不存在的命名或位置参数时，`.Get` 返回一个空字符串而不是中断构建。这使您可以将 `.Get` 与 `if`、`with`、`default` 或 `cond` 链接在一起来检查参数是否存在。例如：

```go-html-template
{{ $quality := default "100" (.Get 1) }}
```

## 另请参阅

- [Create Your Own Shortcodes](https://gohugo.io/templates/shortcode-templates/)
- [Shortcode Variables](https://gohugo.io/variables/shortcodes/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
