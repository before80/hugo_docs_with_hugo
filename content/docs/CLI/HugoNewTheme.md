+++
title = "hugo new theme"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo new theme

[https://gohugo.io/commands/hugo_new_theme/](https://gohugo.io/commands/hugo_new_theme/)

## hugo new theme 

​	创建一个新的主题  

### 概要

​	在`./themes`中创建一个名为`[name]`的新主题（框架）。新主题是一个框架，请在相关文件中添加内容。在许可证的版权行中添加您的名字，并根据需要调整`theme.toml`文件。

```
hugo new theme [name] [flags]
```

### 选项 

```
	  --clock string               设置Hugo使用的时钟，例如：--clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         构建环境
  -h, --help                       帮助主题
      --ignoreVendorPaths string   忽略与给定Glob模式匹配的模块路径中的任何_vendor
  -s, --source string              从文件系统路径读取文件的路径
      --themesDir string           主题目录的文件系统路径
```

### 从父命令继承的选项

```
      --config string      配置文件 (默认为hugo.yaml|json|toml)
      --configDir string   配置目录 (默认为“config”)
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，自动启用日志记录）
      --quiet              静默模式构建
  -v, --verbose            详细输出
      --verboseLog         详细日志记录
```

### 另请参阅 

- [hugo new](https://gohugo.io/commands/hugo_new/) - 为您的站点创建新内容

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
