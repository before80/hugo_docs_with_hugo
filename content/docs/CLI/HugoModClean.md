+++
title = "hugo mod clean"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod clean

[https://gohugo.io/commands/hugo_mod_clean/](https://gohugo.io/commands/hugo_mod_clean/)

## hugo mod clean 

​	删除当前项目的Hugo模块缓存。  

### 概要

​	删除当前项目的Hugo模块缓存。  

​	请注意，运行此命令后，所有依赖项将在下次运行"hugo"时重新下载。  

​	还要注意，如果为"modules"文件缓存配置了正的maxAge，则也将在"hugo –gc"中清除它。

```
hugo mod clean [flags]
```

### 选项 

```
      --all              清除整个模块缓存
  -h, --help             清除帮助
      --pattern string   匹配要清除的模块路径的模式（如果未设置，则为全部），例如“**hugo*”	
```

### 从父命令继承的选项

```
	  --clock string               设置Hugo使用的时钟，例如--clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略匹配给定Glob模式的模块路径的任何_vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，自动启用日志记录）
      --quiet                      安静模式构建
  -s, --source string              从文件系统路径读取文件的相对路径
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    冗长输出
      --verboseLog                 详细日志记录
```

### 另请参阅 

- [hugo mod](https://gohugo.io/commands/hugo_mod/) - 各种Hugo模块助手.

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
