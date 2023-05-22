+++
title = "使用 Hugo 模块"
weight = 2
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Use Hugo Modules - 使用 Hugo 模块 

https://gohugo.io/hugo-modules/use-modules/

​	如何使用 Hugo 模块来构建和管理您的站点。

## 先决条件 

​	大多数 Hugo 模块的命令需要安装更新版本的 Go（请参阅 [https://golang.org/dl/](https://golang.org/dl/)）和相关的 VCS 客户端（例如 Git，请参阅 [https://git-scm.com/downloads/](https://git-scm.com/downloads/)）。如果您在 Netlify 上运行的是"旧"站点，则可能需要在环境设置中将 GO_VERSION 设置为 1.12。

​	有关 Go 模块的更多信息，请参见:

- [https://github.com/golang/go/wiki/Modules](https://github.com/golang/go/wiki/Modules)
- [https://blog.golang.org/using-go-modules](https://blog.golang.org/using-go-modules)

## 初始化新模块 

​	使用 `hugo mod init` 初始化一个新的 Hugo 模块。如果它无法猜测模块路径，您必须提供它作为参数，例如:

```bash
hugo mod init github.com/gohugoio/myShortcodes
```

​	另请参阅 [CLI 文档](https://gohugo.io/commands/hugo_mod_init/)。

## 为主题使用模块 

​	使用模块作为主题的最简单方法是在配置中导入它。

1. 初始化 hugo 模块系统：`hugo mod init github.com/<your_user>/<your_project>` 
2. 导入主题：

config.

=== "yaml"

    ```yaml
    module:
      imports:
      - path: github.com/spf13/hyde
    ```

=== "toml"

    ```toml
    [module]
    [[module.imports]]
      path = 'github.com/spf13/hyde'
    ```

=== "json"

    ```json
    {
       "module": {
          "imports": [
             {
                "path": "github.com/spf13/hyde"
             }
          ]
       }
    }
    ```



## 更新模块 

​	将模块作为导入项添加到您的配置文件时，模块将被下载并添加，详见[模块导入](https://gohugo.io/hugo-modules/configuration/#module-config-imports)。

​	要更新或管理版本，可以使用 `hugo mod get` 命令。

​	以下是一些示例：

### 更新所有模块 

```bash
hugo mod get -u
```

### 递归更新所有模块 

```bash
hugo mod get -u ./...
```

### 更新一个模块 

```bash
hugo mod get -u github.com/gohugoio/myShortcodes
```

### 获取特定版本 

```bash
hugo mod get github.com/gohugoio/myShortcodes@v1.0.7
```

​	另请参阅 [CLI 文档](https://gohugo.io/commands/hugo_mod_get/)。

## 在模块中进行更改和测试 

​	在项目中导入模块并进行本地开发的一种方法是在 `go.mod` 中使用replace 指令将本地目录与源代码联系起来：

```bash
replace github.com/bep/hugotestmods/mypartials => /Users/bep/hugotestmods/mypartials
```

​	如果 `hugo server`正在运行，则会重新加载配置，并将 `/Users/bep/hugotestmods/mypartials` 添加到监视列表中。

​	除了修改 `go.mod` 文件之外，您还可以使用模块配置的[replacements](https://gohugo.io/hugo-modules/configuration/#module-config-top-level)选项。

## 打印依赖项图 

​	从相关的模块目录使用 `hugo mod graph` 命令，它将打印依赖项图，包括 vendoring、模块替换或禁用状态。

E.g.:

```bash
hugo mod graph

github.com/bep/my-modular-site github.com/bep/hugotestmods/mymounts@v1.2.0
github.com/bep/my-modular-site github.com/bep/hugotestmods/mypartials@v1.0.7
github.com/bep/hugotestmods/mypartials@v1.0.7 github.com/bep/hugotestmods/myassets@v1.0.4
github.com/bep/hugotestmods/mypartials@v1.0.7 github.com/bep/hugotestmods/myv2@v1.0.0
DISABLED github.com/bep/my-modular-site github.com/spf13/hyde@v0.0.0-20190427180251-e36f5799b396
github.com/bep/my-modular-site github.com/bep/hugo-fresh@v1.0.1
github.com/bep/my-modular-site in-themesdir
```

​	另请参阅 [CLI 文档](https://gohugo.io/commands/hugo_mod_graph/)。

## Vendor Your Modules 

​	运行`hugo mod vendor`将所有模块依赖项写入`_vendor`文件夹，然后在所有后续构建中使用它们。

请注意：

- 您可以在模块树的任何级别上运行 `hugo mod vendor`。 
- 存储在`themes`文件夹中的模块不会被存储到Vendoring目录中。 
- 大多数命令接受`--ignoreVendorPaths`标志，然后不会对与给定[Glob](https://github.com/gobwas/glob)模式匹配的模块路径使用`_vendor`中的供应商模块。 

​	另请参阅[CLI文档](https://gohugo.io/commands/hugo_mod_vendor/)。

## 整理go.mod、go.sum 

​	运行 `hugo mod tidy` 以删除 `go.mod` 和 `go.sum` 中未使用的条目。

​	另请参阅[CLI文档](https://gohugo.io/commands/hugo_mod_clean/)。

## 清除模块缓存 

​	运行 `hugo mod clean` 以删除整个模块缓存。

​	请注意，您还可以通过 `maxAge` 配置模块缓存，请参阅[文件缓存](https://gohugo.io/getting-started/configuration/#configure-file-caches)。

​	另请参阅[CLI文档](https://gohugo.io/commands/hugo_mod_clean/)。

## 模块工作区 

[New in v0.109.0](https://github.com/gohugoio/hugo/releases/tag/v0.109.0)

​	[Go 1.18](https://go.dev/blog/get-familiar-with-workspaces) 版本中增加了工作区支持，而 Hugo 在 v0.109.0 版本中得到了稳定的支持。

​	工作区的常见用途是简化带有其主题模块的站点的本地开发。

​	可以在 `*.work` 文件中配置工作区，并通过 [module.workspace](https://gohugo.io/hugo-modules/configuration/) 设置激活它，对于此用法下通常由 `HUGO_MODULE_WORKSPACE` 操作系统环境变量控制。

​	在Hugo 文档库中查看[hugo.work](https://github.com/gohugoio/hugo/blob/master/hugo.work)文件以获取示例：

```
go 1.19

use .
use ../gohugoioTheme
```

​	使用 `use` 指令，列出您要处理的所有模块，指向其相对位置。如上例所示，建议始终在列表中包括主项目（"`.`"）。

​	有了这个指令，您可以使用启用了该工作区的Hugo服务器：

```
HUGO_MODULE_WORKSPACE=hugo.work hugo server --ignoreVendorPaths "**"
```

​	上面添加了 `--ignoreVendorPaths` 标志，以忽略 `_vendor` 中与给定 Glob 模式匹配的模块路径中的任何存储的依赖项。如果您不使用 vendoring，则不需要该标志。但现在，服务器设置为监视工作区中的文件和目录，您可以看到重新加载本地编辑。

## 另请参阅 

- [配置模块 ](https://gohugo.io/hugo-modules/configuration/)
- [主题组件 ](https://gohugo.io/hugo-modules/theme-components/)
- [目录结构 ](https://gohugo.io/getting-started/directory-structure/)
- [静态文件 ](https://gohugo.io/content-management/static-files/)
- [将您的Hugo主题添加到展示窗口](https://gohugo.io/contribute/themes/)
