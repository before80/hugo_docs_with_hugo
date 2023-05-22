+++
title = "ContentTypes"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Content Types - 内容类型 

[https://gohugo.io/content-management/types/](https://gohugo.io/content-management/types/)

Hugo is built around content organized in sections.

​	Hugo 建立在按章节组织内容的基础上。 

​	内容类型是组织内容的一种方式。Hugo 会根据正文中的类型或者文件路径中的第一个目录（如果没有设置类型）来确定内容类型。例如，如果没有设置类型，则 `content/blog/my-first-event.md` 将被认为是类型为`blog`的内容。

​	内容类型用于：

- 确定如何渲染内容。了解更多请参见[模板查找顺序](https://gohugo.io/templates/lookup-order/)和[内容视图](https://gohugo.io/templates/views)。 
- 确定要用于新内容的[原型](https://gohugo.io/content-management/archetypes/)模板。 

## 另请参阅 

- [内容章节](https://gohugo.io/content-management/sections/)
- [.GetPage](https://gohugo.io/functions/getpage/)
- [Comments](https://gohugo.io/content-management/comments/)
- [内容组织 ](https://gohugo.io/content-management/organization/)
- [Hugo 中的内容列表](https://gohugo.io/templates/lists/)
