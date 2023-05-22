+++
title = "hugo gen doc"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo gen doc

[https://gohugo.io/commands/hugo_gen_doc/](https://gohugo.io/commands/hugo_gen_doc/)

## hugo gen doc 

Generate Markdown documentation for the Hu CLI.

​	为 Hugo CLI 生成 Markdown 文档。  

### 概要

​	为 Hugo CLI 生成 Markdown 文档。  

​	这个命令主要用于为 [https://gohugo.io/](https://gohugo.io/ ) 的 Hugo 命令行接口创建最新的文档。  

​	它为每个命令创建一个带有适合在 Hugo 中渲染的前置元数据的 Markdown 文件。

```
hugo gen doc [flags]
```

### 选项 

```
      --dir string   要写入文档的目录。(默认值为 "/tmp/hugodoc/")
  -h, --help         help for doc
```

### 从父命令继承的选项

```
--clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认值为 "config"）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的任何 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，日志记录将自动启用）
      --quiet                      静默模式构建
  -s, --source string              从中读取文件的文件系统路径
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    冗长输出
      --verboseLog                 冗长日志
```

### 另请参阅 

- [hugo gen](https://gohugo.io/commands/hugo_gen/) - 一个包含多个有用生成器的集合。 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
