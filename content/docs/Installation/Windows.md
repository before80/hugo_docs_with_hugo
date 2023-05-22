+++
title = "Windows"
weight = 3
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# Windows

[https://gohugo.io/installation/windows/](https://gohugo.io/installation/windows/)

​	在 Windows 上安装 Hugo。 

## 版本

​	Hugo 有两个版本：标准版和扩展版。使用扩展版，您可以：

- 将 WebP 图像进行编码（标准版和扩展版都可以解码 WebP 图像） 
- 使用内置的 LibSass 转译器将 Sass 转译为 CSS 

​	我们建议您安装扩展版。

## 先决条件 

​	虽然在某些情况下不是必需的，但在使用 Hugo 时经常使用 Git 和 Go。

​	需要Git的情况：

- 使用[Hugo Modules](https://gohugo.io/hugo-modules/)功能 
- 从源代码构建Hugo 
- 将主题安装为Git子模块 
- 从本地Git存储库访问[提交信息](https://gohugo.io/variables/git) 
- 使用服务托管您的站点，例如[AWS Amplify](https://aws.amazon.com/amplify/)、[CloudCannon](https://cloudcannon.com/)、[Cloudflare Pages](https://pages.cloudflare.com/)、[GitHub Pages](https://pages.github.com/)、[GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/)和[Netlify](https://www.netlify.com/)。

​	需要Go的情况：

- 使用Hugo Modules功能 
- 从源代码构建Hugo

​	请参阅[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)和[Go](https://go.dev/doc/install)文档以获取安装说明。

## 预构建二进制文件 

​	预构建的二进制文件可用于各种操作系统和架构。访问[最新版本](https://github.com/gohugoio/hugo/releases/latest)页面，然后向下滚动到Assets 部分。

1. 下载所需[版本](https://gohugo.io/installation/linux/#editions)、操作系统和架构的存档 
2. 解压缩存档 
3. 将可执行文件移动到所需目录 
4. 将此目录添加到PATH环境变量中 
5. 验证您对该文件具有执行权限 

​	如果需要帮助设置文件权限或修改PATH环境变量，请参考操作系统文档。

​	如果您没有看到所需版本、操作系统和架构的预构建二进制文件，请使用以下方法之一安装Hugo。

## 包管理器 

### Chocolatey 

​	[Chocolatey](https://chocolatey.org/)是 Windows 的一个免费开源软件包管理器。这将安装 Hugo 的扩展版：

```sh
choco install hugo-extended
```

### Scoop 

​	[Scoop](https://scoop.sh/)是 Windows 的一个免费开源软件包管理器。这将安装 Hugo 的扩展版：

```sh
scoop install hugo-extended
```

### Winget 

​	[Winget](https://learn.microsoft.com/en-us/windows/package-manager/)是微软的官方免费开源软件包管理器。这将安装 Hugo 的扩展版：

```sh
winget install Hugo.Hugo.Extended
```

## Docker 

​	[Erlend Klakegg Bergheim](https://github.com/klakegg) 慷慨地维护基于 Alpine Linux、Busybox、Debian 和 Ubuntu 的 [Docker 映像](https://hub.docker.com/r/klakegg/hugo)。

```sh
docker pull klakegg/hugo
```

## 从源代码构建 

要从源代码构建 Hugo，您必须：

1. 安装[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
2. 安装 [Go](https://go.dev/doc/install) 版本 1.18 或更高版本 
3. 按照 [Go 文档](https://go.dev/doc/code#Command)中的说明更新 PATH 环境变量。

> ​	安装目录由GOPATH和GOBIN环境变量控制。如果设置了GOBIN，则二进制文件将安装到该目录。如果设置了GOPATH，则二进制文件将安装到GOPATH列表中第一个目录的bin子目录中。否则，二进制文件将安装到默认的GOPATH的bin子目录中（`$HOME/go`或`%USERPROFILE%\go`）。

​	然后进行构建和测试：

```sh
go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```

​	在Windows上构建Hugo的扩展版时，还需要安装[GCC编译器](https://gcc.gnu.org/)。请参考这些[详细的说明](https://discourse.gohugo.io/t/41370)。

## 比较

|                           | Prebuilt binaries |                  Package managers                   |                       Docker                        | Build from source |      |
| :------------------------ | :---------------: | :-------------------------------------------------: | :-------------------------------------------------: | :---------------: | :--- |
| Easy to install?          |         ✔️         |                          ✔️                          |                          ✔️                          |         ✔️         |      |
| Easy to upgrade?          |         ✔️         |                          ✔️                          |                          ✔️                          |         ✔️         |      |
| Easy to downgrade?        |         ✔️         | ✔️ [1](https://gohugo.io/installation/windows/#fn:1) |                          ✔️                          |         ✔️         |      |
| Automatic updates?        |         ❌         | ❌ [2](https://gohugo.io/installation/windows/#fn:2) | ❌ [2](https://gohugo.io/installation/windows/#fn:2) |         ❌         |      |
| Latest version available? |         ✔️         |                          ✔️                          |                          ✔️                          |         ✔️         |      |

------

1. 如果先前安装了旧版本，则易于安装。↩︎
2. 可能，但需要高级配置。↩︎ ↩︎

## See 另请参阅 

- [Linux](https://gohugo.io/installation/linux/)
- [macOS](https://gohugo.io/installation/macos/)
- [BSD](https://gohugo.io/installation/bsd/)
- [在21YunBox上托管 ](https://gohugo.io/hosting-and-deployment/hosting-on-21yunbox/)
- [在 GitHub 上托管](https://gohugo.io/hosting-and-deployment/hosting-on-github/)