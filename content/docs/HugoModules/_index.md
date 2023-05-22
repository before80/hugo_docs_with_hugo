+++
title = "Hugo模块"
linkTitle = "Hugo模块"
weight = 4
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Hugo Modules - Hugo 模块

https://gohugo.io/hugo-modules/

​	Hugo 模块是 Hugo 的核心构建块。一个模块可以是您的主项目或一个较小的模块，提供 Hugo 中定义的 7 种组件类型之一或多个组件类型：**static**， **content**， **layouts**，**data**， **assets**， **i18n** 和**archetypes**。

​	您可以以任何组合方式组合模块，甚至挂载来自非 Hugo 项目的目录，形成一个大的虚拟联合文件系统。

​	Hugo 模块由 Go 模块驱动。有关 Go 模块的更多信息，请参见：

- https://github.com/golang/go/wiki/Modules
- https://go.dev/blog/using-go-modules

​	这一切都是全新的，只有很少几个示例项目：

- https://github.com/bep/docuapi 是一个主题，已被移植到 Hugo 模块中进行测试。它是一个挂载到 Hugo 文件夹结构中的非 Hugo 项目的很好的例子。它甚至展示了在常规 Go 模板中实现 JS Bundler。
- https://github.com/bep/my-modular-site 是一个非常简单的用于测试的站点。