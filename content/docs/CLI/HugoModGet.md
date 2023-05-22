+++
title = "hugo mod get"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod get

[https://gohugo.io/commands/hugo_mod_get/](https://gohugo.io/commands/hugo_mod_get/)

## hugo mod get 

​	解析您当前 Hugo 项目的依赖项。  

### 概要

​	解析您当前 Hugo 项目的依赖项。  

​	以下是一些示例：  

​	安装给定模块的最新版本：

```
hugo mod get github.com/gohugoio/testshortcodes
```

​	安装特定版本：

```
hugo mod get github.com/gohugoio/testshortcodes@v0.3.0
```

​	安装所有模块依赖的最新版本：

```
hugo mod get -u
hugo mod get -u ./... (recursive)
```

​	运行 "go help get" 以获取更多信息。所有 "go get" 可用的标志在此处也是相关的。  

​	请注意，Hugo将始终首先解析站点配置中定义的组件，这些组件由_vendor目录（如果没有提供`-ignoreVendorPaths`标志）、Go模块或主题目录内的文件夹提供，按照此顺序解析。

​	有关详细信息，请参阅 [https://gohugo.io/hugo-modules/](https://gohugo.io/hugo-modules/)。

```
hugo mod get [flags]
```

### 选项 

```
  -h, --help   help for get
```

### 从父命令继承的选项

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为 "config"）
      --debug                      调试输出
  -e，--environment string         构建环境
      --ignoreVendorPaths string   忽略匹配给定 Glob 模式的模块路径的任何 _vendor 
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，自动启用日志记录）
      --quiet                      安静模式下构建
  -s，--source string              从文件系统路径读取文件，相对路径
      --themesDir string           主题目录的文件系统路径
  -v，--verbose                    输出详细信息
      --verboseLog                 输出详细日志
```

### 另请参阅 

- [hugo mod](https://gohugo.io/commands/hugo_mod/) - 各种 Hugo 模块助手。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
