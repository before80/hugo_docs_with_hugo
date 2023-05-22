+++
title = "hugo convert toTOML"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo convert toTOML

[https://gohugo.io/commands/hugo_convert_totoml/](https://gohugo.io/commands/hugo_convert_totoml/)

## hugo convert toTOML 

​	将前置元数据转换为 TOML格式。  

### 概要

​	toTOML 将内容目录中的所有前置元数据转换为使用 TOML 格式的前置元数据。

```
hugo convert toTOML [flags]
```

### 选项 

```
  -h, --help   help for toTOML
```

### 从父命令继承的选项

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的任何 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，将自动启用日志记录）
  -o, --output string              写入文件的文件系统路径
      --quiet                      静音模式下进行构建
  -s, --source string              从文件系统路径读取与文件相关的文件
      --themesDir string           主题目录的文件系统路径
      --unsafe                     启用更少安全的操作，请先备份
  -v, --verbose                    详细输出
      --verboseLog                 详细日志记录
```

### 另请参阅 

- [hugo convert](https://gohugo.io/commands/hugo_convert/) - Convert your content to different formats

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
