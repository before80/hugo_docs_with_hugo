+++
title = "Linux"
weight = 2
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# Linux

https://gohugo.io/installation/linux/

​	在Linux上安装Hugo。

## 版本 

​	Hugo有两个版本：标准版和扩展版。使用扩展版可以：

- 编码WebP图像（使用两个版本都可以解码WebP图像） 
- 使用内置的LibSass编译器将Sass转换为CSS 

​	我们建议您安装扩展版。

## 前提条件 

​	虽然并非所有情况下都需要，但在使用Hugo时通常使用Git和Go。

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

### Snap 

​	[Snap](https://snapcraft.io/)是Linux的免费开源软件包管理器。Snap包适用于大多数发行版，易于安装并且会自动更新。

​	Hugo snap包是[严格隔离的](https://snapcraft.io/docs/snap-confinement)。严格隔离的snap运行在完全隔离的环境中，最小访问级别被认为是始终安全的。您创建和构建的站点必须位于您的主目录内或可移动媒体上。

​	这将安装Hugo的扩展版：

```sh
sudo snap install hugo
```

### Homebrew 

​	[Homebrew](https://brew.sh/)是macOS和Linux的免费开源软件包管理器。这将安装Hugo的扩展版：

```sh
brew install hugo
```

## 存储库包 

​	大多数Linux发行版都维护着一个通用安装应用程序的软件仓库。请注意，这些仓库可能不包含[最新版本](https://github.com/gohugoio/hugo/releases/latest)。

### Arch Linux 

​	基于[Arch Linux](https://archlinux.org/)的Linux发行版包括[EndeavourOS](https://endeavouros.com/)，[Garuda Linux](https://garudalinux.org/)，[Manjaro](https://manjaro.org/)等。这将安装Hugo的扩展版：

```sh
sudo pacman -S hugo
```

### Debian 

​	基于[Debian](https://www.debian.org/)的Linux发行版包括[elementary OS](https://elementary.io/)，[KDE neon](https://neon.kde.org/)，[Linux Lite](https://www.linuxliteos.com/)，[Linux Mint](https://linuxmint.com/)，[MX Linux](https://mxlinux.org/)，[Pop!_OS](https://pop.system76.com/)，[Ubuntu](https://ubuntu.com/)，[Zorin OS](https://zorin.com/os/)等。这将安装Hugo的扩展版：

```sh
sudo apt install hugo
```

​	您也可以从[最新版本](https://github.com/gohugoio/hugo/releases/latest)页面下载Debian包。

### Fedora 

​	基于[Fedora](https://getfedora.org/)的Linux发行版包括[CentOS](https://www.centos.org/)，[Red Hat Enterprise Linux](https://www.redhat.com/)等。这将安装Hugo的扩展版：

```sh
sudo dnf install hugo
```

### openSUSE 

​	基于[openSUSE](https://www.opensuse.org/)的Linux发行版包括[GeckoLinux](https://geckolinux.github.io/)，[Linux Karmada](https://linuxkamarada.com/)等。这将安装Hugo的扩展版：

```sh
sudo zypper install hugo
```

### Solus 

​	Solus的Linux发行版在其包存储库中包含Hugo。这将安装Hugo的标准版：

```sh
sudo eopkg install hugo
```

## Docker 

​	[Erlend Klakegg Bergheim](https://github.com/klakegg)慷慨地维护了基于Alpine Linux、Busybox、Debian和Ubuntu的[Docker images](https://hub.docker.com/r/klakegg/hugo)。

```sh
docker pull klakegg/hugo
```

## 从源代码构建 

​	要从源代码构建Hugo，您必须：

1. 安装 [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
2. 安装[Go](https://go.dev/doc/install)版本1.18或更高版本 
3. 按[Go文档](https://go.dev/doc/code#Command)中的说明更新PATH环境变量 

> 安装目录由GOPATH和GOBIN环境变量控制。如果设置了GOBIN，那么二进制文件将安装到该目录中。如果设置了GOPATH，则二进制文件将安装到GOPATH列表中第一个目录的bin子目录中。否则，二进制文件将安装到默认GOPATH的bin子目录（`$HOME/go`或`%USERPROFILE%\go`）。

然后构建和测试：

```sh
go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```

## 对比

|                           | Prebuilt binaries |                    Package managers                    | Repository packages |                      Docker                       | Build from source |
| :------------------------ | :---------------: | :----------------------------------------------------: | :-----------------: | :-----------------------------------------------: | :---------------: |
| Easy to install?          |         ✔️         |                           ✔️                            |          ✔️          |                         ✔️                         |         ✔️         |
| Easy to upgrade?          |         ✔️         |                           ✔️                            |       varies        |                         ✔️                         |         ✔️         |
| Easy to downgrade?        |         ✔️         |   ✔️ [1](https://gohugo.io/installation/linux/#fn:1)    |       varies        |                         ✔️                         |         ✔️         |
| Automatic updates?        |         ❌         | varies [2](https://gohugo.io/installation/linux/#fn:2) |          ❌          | ❌ [3](https://gohugo.io/installation/linux/#fn:3) |         ❌         |
| Latest version available? |         ✔️         |                           ✔️                            |       varies        |                         ✔️                         |         ✔️         |

------

1. 如果之前安装了旧版本，安装将变得容易。 ↩︎
2. Snap 包会自动更新。Homebrew 需要高级配置。 ↩︎
3. 虽然可能，但需要高级配置。 ↩︎

## 另请参阅

- [macOS](https://gohugo.io/installation/macos/)
- [Windows](https://gohugo.io/installation/windows/)
- [BSD](https://gohugo.io/installation/bsd/)
- [在21YunBox上托管 ](https://gohugo.io/hosting-and-deployment/hosting-on-21yunbox/)
- [在 GitHub 上托管](https://gohugo.io/hosting-and-deployment/hosting-on-github/)