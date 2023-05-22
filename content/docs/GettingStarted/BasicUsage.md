+++
title = "基础用法"
weight = 2
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# Basic usage - 基础用法 

[https://gohugo.io/getting-started/usage/](https://gohugo.io/getting-started/usage/)

​	Hugo的命令行界面（CLI）功能齐全但简单易用，即使对于那些在命令行上有限经验的人也是如此。 

## 测试您的安装 

​	[安装](https://gohugo.io/installation/)完Hugo后，请通过运行以下命令来测试您的安装：

```bash
hugo version
```

​	您应该会看到类似于以下的输出：

```text
hugo v0.105.0-0e3b42b4a9bdeb4d866210819fc6ddcf51582ffa+extended linux/amd64 BuildDate=2022-10-28T12:29:05Z VendorInfo=snap:0.105.0
```

## 显示可用命令 

​	要查看可用命令和标志的列表：

```bash
hugo help
```

​	要获取子命令的帮助，请使用`--help`标志。例如：

```bash
hugo server --help
```

## 构建您的站点 

​	要构建您的站点，请`cd`进入您的项目目录并运行：

```bash
hugo
```

​	`hugo`命令将构建您的站点，将文件发布到`public`目录中。要将您的站点发布到不同的目录中，请使用`--destination`标志**或**在您的站点配置中设置`publishDir`。

​	Hugo在构建您的站点之前不会清除`public`目录。现有的文件将被覆盖，但不会被删除。这种行为是有意的，以防止意外删除您在构建之后添加到`public`目录中的文件。

​	根据您的需求，您可能希望在每次构建之前手动清除public目录的内容。

## 草稿、未来和过期内容 

​	Hugo允许您在内容的[前置元数据](https://gohugo.io/content-management/front-matter/)中设置`draft`、`date`、`publishDate`和`expiryDate`。默认情况下，Hugo不会发布以下内容：

- `draft`值为`true`时 
- `date`在未来时 
- `publishDate`在未来时 
- `expiryDate`在过去时

​	您可以在运行`hugo`或`hugo server`时使用命令行标志来覆盖默认行为：

```bash
hugo --buildDrafts    # or -D
hugo --buildExpired   # or -E
hugo --buildFuture    # or -F
```

​	尽管您也可以在站点配置中设置这些值，但除非所有内容作者都知道并理解这些设置，否则可能会导致意想不到的结果。

​	正如上面所述，Hugo 在构建站点之前不会清除 `public` 目录。根据上述四个条件的当前评估，构建后您的 `public` 目录可能包含来自上一次构建的不必要的文件。

​	一种常见的做法是在每次构建之前手动清除 `public` 目录的内容，以删除草稿、过期和未来的内容。

## 开发和测试您的站点

​	为了在开发布局或创建内容时查看您的站点，请`cd`进入项目目录并运行：

```bash
hugo server
```

​	`hugo server` 命令将您的站点构建到内存中，并使用最小的 HTTP 服务器提供您的页面。运行 `hugo server` 时，它将显示您本地站点的 URL：

```text
Web Server is available at http://localhost:1313/ 
```

​	在服务器运行时，它会监视项目目录中的资源、配置、内容、数据、布局、翻译和静态文件的更改。当它检测到更改时，服务器会重新构建您的站点并使用 [LiveReload](https://github.com/livereload/livereload-js)刷新您的浏览器。

​	大多数 Hugo 构建速度都非常快，除非您直接查看浏览器，否则可能不会注意到更改。

### LiveReload 

​	在服务器运行时，Hugo 会将 JavaScript 注入生成的 HTML 页面中。LiveReload 脚本通过 Web sockets 创建了一个从浏览器到服务器的连接。您不需要安装任何软件或浏览器插件，也不需要任何配置。

### 自动重定向

​	当编辑内容时，如果您希望浏览器自动重定向到您最后修改的页面，请运行：

```bash
hugo server --navigateToChanged
```

## 部署您的站点 

​	如上所述，Hugo 在构建站点之前不会清空 public 目录。在每次构建之前手动清空 public 目录以删除草稿、已过期和未来的内容。

​	当您准备部署您的站点时，运行：

```bash
hugo
```

​	这会构建您的站点，并将文件发布到 `public` 目录。目录结构将类似于：

```text
public/
├── categories/
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── post/
│   ├── my-first-post/
│   │   └── index.html
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── tags/
│   ├── index.html
│   └── index.xml  <-- RSS feed for this section
├── index.html
├── index.xml      <-- RSS feed for the site
└── sitemap.xml
```

​	在一个简单的托管环境中，您通常会通过 `ftp`、`rsync` 或 `scp` 将您的文件传输到虚拟主机的根目录，`public` 目录的内容就是您所需的全部内容。

​	我们的大多数用户使用 CI/CD 工作流部署其站点，其中对 GitHub 或 GitLab 存储库的推送触发了构建和部署。流行的提供者包括 [AWS Amplify](https://aws.amazon.com/amplify/)， [CloudCannon](https://cloudcannon.com/)， [Cloudflare Pages](https://pages.cloudflare.com/)， [GitHub Pages](https://pages.github.com/)， [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/)和 [Netlify](https://www.netlify.com/)。

​	在[托管和部署](https://gohugo.io/hosting-and-deployment/)部分中了解更多信息。

------

1. Git 存储库包含整个项目目录，通常不包括 public 目录，因为在push之后才构建站点。↩︎

## 另请参阅  

- [外部学习资源](https://gohugo.io/getting-started/external-learning-resources/)
- [快速入门](https://gohugo.io/getting-started/quick-start/)
- [使用 Hugo 模块](https://gohugo.io/hugo-modules/use-modules/)