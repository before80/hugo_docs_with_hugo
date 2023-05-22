+++
title = "hugo mod npm pack"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod npm pack

[https://gohugo.io/commands/hugo_mod_npm_pack/](https://gohugo.io/commands/hugo_mod_npm_pack/)

## hugo mod npm pack 

​	实验性功能：准备并写入项目的组合 package.json 文件。

### 概要

​	准备并写入项目的组合 package.json 文件。

​	第一次运行时，如果项目根目录中没有"package.hugo.json"文件，则会创建该文件。此文件将用作具有基本依赖项集合的模板文件。

​	该集合将与在依赖树中找到的所有"package.hugo.json"文件合并，选择最接近项目的版本。

​	此命令标记为 Experimental。我们认为这是一个很好的想法，因此不太可能从 Hugo 中删除，但我们需要在"real life"中进行测试以了解它的感觉，因此在未来的Hugo版本中它可能会/将更改。

```
hugo mod npm pack [flags]
```

### 选项 

```
  -h, --help   help for pack
```

### 从父命令继承的选项

```
      --clock string               设置 Hugo 使用的时钟，例如--clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认值为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径中的任何 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，则自动启用日志记录）
      --quiet                      静默模式下构建
  -s, --source string              从文件系统路径读取相对文件
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    详细输出
      --verboseLog                 详细日志记录

```

### 另请参阅 

- [hugo mod npm](https://gohugo.io/commands/hugo_mod_npm/) - 各种 npm 助手。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
