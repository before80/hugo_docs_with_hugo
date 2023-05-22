+++
title = "hugo gen man"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo gen man

[https://gohugo.io/commands/hugo_gen_man/](https://gohugo.io/commands/hugo_gen_man/)

## hugo gen man 

​	为 Hugo CLI 生成 man 页面

### 概要

​	该命令可以自动生成最新版本的Hugo CLI 的man页。默认情况下，它会在当前目录下的"man"目录中创建man页文件。

```
hugo gen man [flags]
```

### 选项 

```
      --dir string   写入man页的目录 (默认值为 "man/")
  -h, --help         help for man
```

### 从父命令继承的选项

```
      --clock string               设置Hugo使用的时钟，例如--clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件 (默认为 hugo.yaml|json|toml)
      --configDir string           配置目录 (默认为 "config")
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略匹配给定Glob模式的模块路径中的任何_vendor
      --log                        启用日志记录
      --logFile string             日志文件路径 (如果设置，则自动启用日志记录)
      --quiet                      静默模式构建
  -s, --source string              读取文件的文件系统路径相对于哪里
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    详细输出
      --verboseLog                 详细日志记录

```

### 另请参阅 

- [hugo gen](https://gohugo.io/commands/hugo_gen/) - 一个包含多个有用生成器的集合。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
