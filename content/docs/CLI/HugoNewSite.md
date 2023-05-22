+++
title = "hugo new site"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo new site

[https://gohugo.io/commands/hugo_new_site/](https://gohugo.io/commands/hugo_new_site/)

## hugo new site 

​	创建新站点（框架）

### 概要

​	在指定的目录中创建新站点。新站点将具有正确的结构，但尚未包含任何内容或主题。使用 `hugo new [contentPath]` 创建新的内容。

```
hugo new site [path] [flags]
```

### 选项 

```
      --clock string               设置 Hugo 使用的时钟，例如：--clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         构建环境
      --force                      在非空目录中初始化
  -f, --format string              配置文件格式（默认为 "toml"）
  -h, --help                       site 的帮助信息
      --ignoreVendorPaths string   忽略匹配给定 Glob 模式的模块路径中的任何 _vendor
  -s, --source string              从文件系统路径中读取相对文件的路径
      --themesDir string           主题目录的文件系统路径

```

### 从父命令继承的选项

```
      --config string      配置文件（默认为 hugo.yaml|json|toml）
      --configDir string   配置目录（默认为 "config"）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，则自动启用日志记录）
      --quiet              静默模式下构建
  -v, --verbose            冗长输出
      --verboseLog         冗长的日志记录

```

### 另请参阅 

- [hugo new](https://gohugo.io/commands/hugo_new/) - 为您的站点创建新内容

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
