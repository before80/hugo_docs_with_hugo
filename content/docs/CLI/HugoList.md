+++
title = "hugo list"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo list

[https://gohugo.io/commands/hugo_list/](https://gohugo.io/commands/hugo_list/)

## hugo list 

​	列出各种类型的内容

### 概要

​	列出各种类型的内容。

​	List 命令需要一个子命令，例如 `hugo list drafts`。

### 选项 

```
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         构建环境
  -h, --help                       列出帮助信息
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径中的任何 _vendor 文件夹
  -s, --source string              从文件系统路径读取文件的相对路径
      --themesDir string           主题目录的文件系统路径

```

### 从父命令继承的选项

```
      --config string      配置文件（默认为 hugo.yaml|json|toml）
      --configDir string   配置目录（默认为“config”）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置了该选项，则会自动启用日志记录）
      --quiet              静默模式下构建
  -v, --verbose            输出详细信息
      --verboseLog         输出详细日志记录

```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点
- [hugo list all](https://gohugo.io/commands/hugo_list_all/) - 列出所有文章
- [hugo list drafts](https://gohugo.io/commands/hugo_list_drafts/) - 列出所有草稿
- [hugo list expired](https://gohugo.io/commands/hugo_list_expired/) - 列出所有已过期的文章
- [hugo list future](https://gohugo.io/commands/hugo_list_future/) - 列出所有将来发布的文章

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
