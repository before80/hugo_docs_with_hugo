+++
title = "快速入门"
weight = 1
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# Quick Start - 快速入门 

[https://gohugo.io/getting-started/quick-start/](https://gohugo.io/getting-started/quick-start/)

​	学习如何在几分钟内创建一个 Hugo 站点。 

​	在本教程中，您将会：

1. 创建一个站点 
2. 添加内容 
3. 配置站点 
4. 发布站点 

## 先决条件

​	在开始本教程之前，您必须：

1. [安装 Hugo](https://gohugo.io/installation/)（扩展版） 
2. [安装 Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

​	您还必须熟悉使用命令行操作。

## 创建一个站点 

### 命令

> 如果您是 Windows 用户：
>
> - 不要使用命令提示符 
> - 不要使用 Windows PowerShell 
> - 请在 [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-window) 或类似于 WSL 或 Git Bash 的 Linux 终端中运行这些命令。
>
> PowerShell 和 Windows PowerShell 是不同的应用程序。

​	运行以下命令创建带有 [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke)主题的 Hugo 站点。下一节将对每个命令进行解释。

```bash
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
echo "theme = 'ananke'" >> config.toml
hugo server
```

​	在终端中显示的 URL 上查看您的站点。按 `Ctrl + C` 停止 Hugo 的开发服务器。

### 命令解释 

​	在 `quickstart` 目录中为项目创建[目录结构](https://gohugo.io/getting-started/directory-structure)：

```bash
hugo new site quickstart
```

​	将当前目录切换为项目根目录：

```bash
cd quickstart
```

​	在当前目录中初始化一个空的 Git 存储库：

```bash
git init
```

​	将 [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke)主题克隆到 `themes` 目录中，并将其作为 [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)添加到项目中。

```bash
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
```

​	在站点配置文件中添加一行，指示当前主题：

```bash
echo "theme = 'ananke'" >> config.toml
```

​	启动 Hugo 的开发服务器以查看站点：

```bash
hugo server
```

​	按 `Ctrl + C` 停止 Hugo 的开发服务器。

## 添加内容 

​	在站点中添加一个新页面：

```bash
hugo new posts/my-first-post.md
```

​	Hugo 在 `content/posts` 目录中创建了该文件。使用您的编辑器打开该文件。

```markdown
---
title: "My First Post"
date: 2022-11-20T09:03:20-08:00
draft: true
---
```

​	请注意，[前置元数据](https://gohugo.io/content-management/front-matter)中的`draft`值为 `true`。默认情况下，Hugo 不会在构建站点时发布草稿（draft）内容。了解有关[草稿（draft）、将来（future）和过期（expired）内容](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)的更多信息。

​	在文章的正文中添加一些 [markdown](https://commonmark.org/help/)，但不要更改`draft`的值。

```markdown
---
title: "My First Post"
date: 2022-11-20T09:03:20-08:00
draft: true
---
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```

​	保存文件，然后启动 Hugo 的开发服务器以查看站点。您可以运行以下任一命令来包含草稿内容。

```bash
hugo server --buildDrafts
hugo server -D
```

​	在终端中显示的 URL 上查看您的站点。随着您继续添加和更改内容，请保持开发服务器运行。

> ​	Hugo 的渲染引擎符合 CommonMark 的 markdown [规范](https://spec.commonmark.org/)。CommonMark组织提供了一个有用（由参考实现驱动）的[实时测试工具](https://spec.commonmark.org/dingus/)。

## 配置站点 

​	使用编辑器打开项目根目录中的[站点配置](https://gohugo.io/getting-started/configuration/)文件(`config.toml`)。

```toml
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```

​	进行以下更改：

1. 将`baseURL`设置为您的生产站点。此值必须以协议开头，并以斜杠结尾，如上所示。
2. 将`languageCode`设置为您的语言和地区。
3. 设置生产站点的`title`。

​	启动Hugo的开发服务器以查看更改，记得包括草稿内容。

```text
hugo server -D
```

​	大多数主题作者都会提供配置指南和选项。请务必访问您的主题存储库或文档站点了解详情。

​	Ananke主题的作者[The New Dynamic](https://www.thenewdynamic.com/)为配置和使用提供[文档](https://github.com/theNewDynamic/gohugo-theme-ananke#readme)。他们还提供[演示站点](https://gohugo-ananke-theme-demo.netlify.app/)。

## 发布站点 

​	在此步骤中，您将发布站点，但不会部署它。

​	发布站点时，Hugo会在项目根目录中的`public`目录中创建整个静态站点。这包括HTML文件和assets，如图片、CSS文件和JavaScript文件。

​	在发布站点时，通常不希望包括[草稿（draft）、将来（future）和过期（expired）内容](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)。命令很简单。

```text
hugo
```

​	要了解如何部署站点，请参阅[主机和部署](https://gohugo.io/hosting-and-deployment/)部分。

## 寻求帮助 

​	Hugo的[论坛](https://discourse.gohugo.io/)是一个活跃的用户和开发者社区，他们回答问题、分享知识和提供示例。超过20,000个主题的快速搜索通常可以回答您的问题。请确保在提问之前阅读有关[请求帮助](https://discourse.gohugo.io/t/requesting-help/9132)的信息。

## 其他资源 

​	有关帮助您学习Hugo的其他资源，包括书籍和视频教程，请参见[外部学习资源](https://gohugo.io/getting-started/external-learning-resources/)页面。

## 另请参阅 

- [BSD](https://gohugo.io/installation/bsd/)
- [基本用法](https://gohugo.io/getting-started/usage/) 
- [外部学习资源](https://gohugo.io/getting-started/external-learning-resources/) 
- [在21云盒上托管](https://gohugo.io/hosting-and-deployment/hosting-on-21yunbox/) 
- [在GitHub上托管](https://gohugo.io/hosting-and-deployment/hosting-on-github/)