+++
title = "hugo completion powershell"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo completion powershell



## hugo completion powershell 

​	生成powershell shell的自动补全脚本。  

### 概要

​	生成powershell shell的自动补全脚本。  

​	要在当前的shell会话中加载自动补全：

```
hugo completion powershell | Out-String | Invoke-Expression
```

​	要在每个新会话中加载自动补全，请将上述命令的输出添加到您的 powershell  配置文件中。

```
hugo completion powershell [flags]
```

### 选项 

```
  -h, --help              help for powershell
      --no-descriptions   disable completion descriptions
```

### 从父命令继承的选项

```
	 --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
     --config string              配置文件 (默认为 hugo.yaml|json|toml)
     --configDir string           配置目录 (默认 "config")
     --debug                      调试输出
 -e, --environment string         构建环境
     --ignoreVendorPaths string   忽略任何与给定 Glob 模式匹配的模块路径的 _vendor
     --log                        启用日志记录
     --logFile string             日志文件路径（如果设置，自动启用日志记录）
     --quiet                      安静模式下构建
 -s, --source string              文件系统路径，从中读取相对文件
     --themesDir string           主题目录的文件系统路径
 -v, --verbose                    冗长的输出
     --verboseLog                 冗长的日志记录
```

### 另请参阅 

- [hugo completion](https://gohugo.io/commands/hugo_completion/) - 为指定的shell生成自动完成脚本 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
- [hugo config](https://gohugo.io/commands/hugo_config/)
