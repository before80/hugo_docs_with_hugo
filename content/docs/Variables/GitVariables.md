+++
title = "Git 信息变量"
weight = 8
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Git Info Variables - Git 信息变量 

[https://gohugo.io/variables/git/](https://gohugo.io/variables/git/)

​	获取每个内容文件的最后一次 Git 修订信息。

​	Hugo 的 Git 集成应该是相当高效的，但可能会增加构建时间。这取决于您的 Git 历史记录大小。

## `.GitInfo` 先决条件 

1. Hugo 站点必须位于启用 Git 的目录中。
2. Git 可执行文件必须已安装并在系统 `PATH` 中。
3. 必须在 Hugo 项目中启用 `.GitInfo` 功能，方法是在命令行上传递 `--enableGitInfo` 标志或在 [站点配置文件](https://gohugo.io/getting-started/configuration/) 中将 `enableGitInfo` 设置为 `true`。

## `.GitInfo` 对象 

​	`GitInfo` 对象包含以下字段： 

### .AbbreviatedHash

​	缩写的提交哈希（例如 `866cbcc`）

### .AuthorName

​	作者名称，遵循 [.mailmap](https://git-scm.com/docs/gitmailmap)

### .AuthorEmail

​	作者电子邮件地址，遵循 [.mailmap](https://git-scm.com/docs/gitmailmap)

### .AuthorDate

​	作者日期。 

### .Hash

​	提交哈希（例如 `866cbccdab588b9908887ffd3b4f2667e94090c3`） 

### .Subject

​	提交消息主题（例如， `tpl: Add custom index function`）

## `.Lastmod` 

​	如果启用了 `.GitInfo` 功能，则 `.Lastmod`（在 `Page` 上）从 Git 中获取，即 `.GitInfo.AuthorDate`。可以通过添加自己的 [日期的前置元数据配置](https://gohugo.io/getting-started/configuration/#configure-front-matter) 更改此行为。

## 另请参阅 

- [在 Azure 静态 Web 应用上托管 ](https://gohugo.io/hosting-and-deployment/hosting-on-azure/)
- [在 GitHub 上托管 ](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- [在 GitLab 上托管](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)
