+++
title = "hugo mod init"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod init

[https://gohugo.io/commands/hugo_mod_init/](https://gohugo.io/commands/hugo_mod_init/)

## hugo mod init 

​	将此项目初始化为 Hugo 模块。

### 概要

​	将该项目初始化为 Hugo 模块。它会尝试猜测模块路径，但您也可以通过参数来指定，例如：

```
hugo mod init github.com/gohugoio/testshortcodes
```

​	请注意，Hugo 模块支持多模块项目，因此您可以在 GitHub 的子文件夹中初始化 Hugo 模块，作为一个示例。

```
hugo mod init [flags]
```

### 选项 

```
  -h, --help   help for init
```

### 从父命令继承的选项

```
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略任何 _vendor 目录，以匹配给定的 Glob 模式的模块路径
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，将自动启用日志记录）
      --quiet                      在安静模式下构建
  -s, --source string              从文件系统路径读取文件的相对路径
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    输出详细信息
      --verboseLog                 输出详细的日志记录

```

### 另请参阅 

- [hugo mod](https://gohugo.io/commands/hugo_mod/) - 各种 Hugo 模块助手。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
