+++
title = "配置模块"
weight = 1
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Configure Modules - 配置模块 

[https://gohugo.io/hugo-modules/configuration/](https://gohugo.io/hugo-modules/configuration/)

​	本页描述了模块的配置选项。 

## 模块配置：Top level -> [module]

config.

=== "yaml"

    ```yaml
    module:
      noProxy: none
      noVendor: ""
      private: '*.*'
      proxy: direct
      replacements: ""
      workspace: "off"
    ```

=== "toml"

    ```toml
    [module]
      noProxy = 'none'
      noVendor = ''
      private = '*.*'
      proxy = 'direct'
      replacements = ''
      workspace = 'off'
    ```

=== "json"

    ```json
    {
       "module": {
          "noProxy": "none",
          "noVendor": "",
          "private": "*.*",
          "proxy": "direct",
          "replacements": "",
          "workspace": "off"
       }
    }
    ```



### noVendor

​	一个可选的 Glob 模式，用于匹配在vendoring时跳过的模块路径，例如`"github.com/**"`。 

### vendorClosest

​	当启用时，我们将选择与使用它的模块最接近的vendored模块。默认行为是选择第一个。请注意，每个给定模块路径仍然只能有一个依赖项，因此一旦使用它，就无法重新定义它。 

### proxy

​	定义用于下载远程模块的代理服务器。默认值为 `direct`，表示"git clone"等。 

### noProxy

​	逗号分隔的 glob 列表，匹配不应使用上述配置的代理的路径。 

### private

​	逗号分隔的 glob 列表，匹配应视为私有的路径。 

### workspace

​	要使用的工作区文件。这启用了 Go 工作区模式。请注意，这也可以通过操作系统 env 设置，例如 `export HUGO_MODULE_WORKSPACE=/my/hugo.work`。这仅适用于 Go 1.18+。在 Hugo `v0.109.0` 中，我们将默认设置为 `off`，并且现在会将任何相对的工作文件名解析为相对于工作目录。 

### replacements

​	从模块路径到目录的映射的逗号分隔列表，例如 `github.com/bep/my-theme -> ../..,github.com/bep/shortcodes -> /some/path`。这对于临时本地开发模块非常有用，在这种情况下，您可能希望将其保存为环境变量，例如：`env HUGO_MODULE_REPLACEMENTS="github.com/bep/my-theme -> ../.."`。相对路径相对于 [themesDir](https://gohugo.io/getting-started/configuration/#all-configuration-settings)。允许使用绝对路径。 

​	请注意，上述术语直接映射到 Go 模块中的对应项。设置其中的一些可能会自然地设置为操作系统环境变量。例如，要设置要使用的代理服务器：

```txt
env HUGO_MODULE_PROXY=https://proxy.example.org hugo
```

​	Hugo 模块的大多数命令需要安装更新版本的 Go（请参阅 [https://golang.org/dl/](https://golang.org/dl/)）和相关的 VCS 客户端（例如 Git，请参阅 [https://git-scm.com/downloads/](https://git-scm.com/downloads/)）。如果您在 Netlify 上运行"旧"站点，则可能必须在环境设置中将 GO_VERSION 设置为 1.12。 

​	有关 Go 模块的更多信息，请参见：

- [https://github.com/golang/go/wiki/Modules](https://github.com/golang/go/wiki/Modules)
- [https://blog.golang.org/using-go-modules](https://blog.golang.org/using-go-modules)

## 模块配置：hugoVersion -> [module.hugoVersion]  

​	如果您的模块需要特定版本的Hugo才能正常工作，您可以在`module`部分中指示，并且如果使用过于旧或新的版本，用户将收到警告。

config.

=== "yaml"

    ```yaml
    module:
      hugoVersion:
        extended: false
        max: ""
        min: ""
    ```

=== "toml"

    ```toml
    [module]
      [module.hugoVersion]
        extended = false
        max = ''
        min = ''
    ```

=== "json"

    ```json
    {
       "module": {
          "hugoVersion": {
             "extended": false,
             "max": "",
             "min": ""
          }
       }
    }
    ```

​	以上任何内容均可省略。

### min

​	支持的最低Hugo版本，例如`0.55.0` 

### max

​	支持的最高Hugo版本，例如`0.55.0` 

### extended

​	是否需要Hugo的扩展版本。 

## 模块配置：imports ->[[module.imports]]

config.

=== "yaml"

    ```yaml
    module:
      imports:
      - disable: false
        ignoreConfig: false
        ignoreImports: false
        path: github.com/gohugoio/hugoTestModules1_linux/modh1_2_1v
      - path: my-shortcodes
    ```

=== "toml"

    ```toml
    [module]
    [[module.imports]]
      disable = false
      ignoreConfig = false
      ignoreImports = false
      path = 'github.com/gohugoio/hugoTestModules1_linux/modh1_2_1v'
    [[module.imports]]
      path = 'my-shortcodes'
    ```

=== "json"

    ```json
    {
       "module": {
          "imports": [
             {
                "disable": false,
                "ignoreConfig": false,
                "ignoreImports": false,
                "path": "github.com/gohugoio/hugoTestModules1_linux/modh1_2_1v"
             },
             {
                "path": "my-shortcodes"
             }
          ]
       }
    }
    ```



### path

​	可以是一个有效的 Go 模块路径，例如 `github.com/gohugoio/myShortcodes`，或者是存储在您主题文件夹中的模块目录名称。 

### ignoreConfig

​	如果启用，将不会加载任何模块配置文件，例如 `config.toml`。请注意，这也会停止加载任何传递模块依赖项。 

### ignoreImports

​	如果启用，将不跟随模块导入。 

### disable

​	将其设置为`true`以禁用该模块，同时保留`go.*`文件中的任何版本信息。 

### noMounts

​	不要在此导入中挂载任何文件夹。 

### noVendor

​	永远不要将此导入内容纳入 vendor（仅允许在主项目中）。

​	大多数Hugo模块命令需要安装更新的Go版本（请参见[https://golang.org/dl/](https://golang.org/dl/)）和相关的VCS客户端（例如Git，请参见[https://git-scm.com/downloads/](https://git-scm.com/downloads/)）。如果您在Netlify上运行"旧"站点，则可能需要在环境设置中将GO_VERSION设置为1.12。

​	有关Go模块的更多信息，请参见：

- [https://github.com/golang/go/wiki/Modules](https://github.com/golang/go/wiki/Modules)
- [https://blog.golang.org/using-go-modules](https://blog.golang.org/using-go-modules)

## 模块配置：mounts -> [[module.mounts]]

​	在Hugo 0.56.0中引入`mounts`配置时，我们小心地保留了现有的`contentDir`、`staticDir`等配置，以确保所有现有站点都能继续工作。但是，您不应同时使用两者：如果您添加了`mounts`部分，则应删除旧的`contentDir`、`staticDir`等设置。

​	当您添加mount时，有关目标根目录的默认mount将被忽略：请确保明确添加它。

默认挂载点

config.

=== "yaml"

    ```yaml
    module:
      mounts:
      - source: content
        target: content
      - source: static
        target: static
      - source: layouts
        target: layouts
      - source: data
        target: data
      - source: assets
        target: assets
      - source: i18n
        target: i18n
      - source: archetypes
        target: archetypes
    ```

=== "toml"

    ```toml
    [module]
    [[module.mounts]]
      source = 'content'
      target = 'content'
    [[module.mounts]]
      source = 'static'
      target = 'static'
    [[module.mounts]]
      source = 'layouts'
      target = 'layouts'
    [[module.mounts]]
      source = 'data'
      target = 'data'
    [[module.mounts]]
      source = 'assets'
      target = 'assets'
    [[module.mounts]]
      source = 'i18n'
      target = 'i18n'
    [[module.mounts]]
      source = 'archetypes'
      target = 'archetypes'
    ```

=== "json"

    ```json
    {
       "module": {
          "mounts": [
             {
                "source": "content",
                "target": "content"
             },
             {
                "source": "static",
                "target": "static"
             },
             {
                "source": "layouts",
                "target": "layouts"
             },
             {
                "source": "data",
                "target": "data"
             },
             {
                "source": "assets",
                "target": "assets"
             },
             {
                "source": "i18n",
                "target": "i18n"
             },
             {
                "source": "archetypes",
                "target": "archetypes"
             }
          ]
       }
    }
    ```



### source

挂载点的源目录。对于主项目，可以是相对于项目的路径，也可以是绝对路径，甚至可以是符号链接。对于其他模块，它必须是相对于项目的路径。 

### target

它应该被挂载到Hugo虚拟文件系统中的位置。它必须以Hugo的组件文件夹之一开头：`static`、`content`、`layouts`、`data`、`assets`、`i18n`或`archetypes`。例如，`content/blog`。 

### lang

语言代码，例如"en"。只适用于`content`挂载和多主机模式下的`static`挂载。 

### includeFiles (string or slice)

​	一个或多个用于匹配要包括的文件或目录的[glob（通配符）](https://github.com/gobwas/glob)。如果未设置`excludeFiles`，则与`includeFiles`匹配的文件将被挂载。

​	这些通配符从`source`根开始匹配文件名，它们应该使用Unix样式的斜杠，即使在Windows上也是如此。 `/`匹配挂载点根目录，`**`可以用作超级星号以递归匹配所有目录，例如`/posts/**.jpg`。

​	搜索时忽略大小写。

### excludeFiles (字符串或切片) 

​	一个或多个用于匹配要排除的文件的通配符。

**示例**

config.

=== "yaml"

    ```yaml
    module:
      mounts:
      - excludeFiles: docs/*
        source: content
        target: content
    ```

=== "toml"

    ```toml
    [module]
    [[module.mounts]]
      excludeFiles = 'docs/*'
      source = 'content'
      target = 'content'
    ```

=== "json"

    ```json
    {
       "module": {
          "mounts": [
             {
                "excludeFiles": "docs/*",
                "source": "content",
                "target": "content"
             }
          ]
       }
    }
    ```



## 参见 

- [主题组件 ](https://gohugo.io/hugo-modules/theme-components/)
- [使用Hugo模块](https://gohugo.io/hugo-modules/use-modules/)
- [目录结构](https://gohugo.io/getting-started/directory-structure/)
- [静态文件 ](https://gohugo.io/content-management/static-files/)
- [将您的Hugo主题添加到展示页面](https://gohugo.io/contribute/themes/)
