+++
title = "hugo convert toYAML"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo convert toYAML

[https://gohugo.io/commands/hugo_convert_toyaml/](https://gohugo.io/commands/hugo_convert_toyaml/)

## hugo convert toYAML 

​	将前置元数据转换为 YAML格式。  

### 概要

​	toYAML 将内容目录中的所有前置元数据转换为使用 YAML 格式的前置元数据。

```
hugo convert toYAML [flags]
```

### 选项 

```
  -h, --help   help for toYAML
```

### 从父命令继承的选项

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 匹配的模块路径的 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，日志记录将自动启用）
  -o, --output string              用于写入文件的文件系统路径
      --quiet                      安静模式构建
  -s, --source string              文件系统路径，从中读取文件相对路径
      --themesDir string           文件系统路径，主题目录
      --unsafe                     启用更少安全操作，请首先备份
  -v, --verbose                    详细输出
      --verboseLog                 详细日志记录
```

### 另请参阅 

- [hugo convert](https://gohugo.io/commands/hugo_convert/) - 将您的内容转换为不同的格式 


## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
