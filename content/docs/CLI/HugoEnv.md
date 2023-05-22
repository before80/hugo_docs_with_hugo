+++
title = "hugo env"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo env

[https://gohugo.io/commands/hugo_env/](https://gohugo.io/commands/hugo_env/)

## hugo env 

​	输出Hugo版本和环境信息  

### 概要

​	输出Hugo版本和环境信息。这在Hugo错误报告中非常有用。  

​	如果加上`-v`标志，您将得到一个完整的依赖项列表。

```
hugo env [flags]
```

### 选项 

```
  -h, --help   help for env
```

### 从父命令继承的选项

```
	  --clock string               设置Hugo使用的时钟，例如--clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略任何与给定Glob模式匹配的模块路径的_vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，自动启用日志记录）
      --quiet                      静默模式下构建
  -s, --source string              从文件系统路径读取相对文件
      --themesDir string           文件系统路径到主题目录
  -v, --verbose                    详细输出
      --verboseLog                 详细记录日志
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - 构建您的站点

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
