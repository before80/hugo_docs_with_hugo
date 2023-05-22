+++
title = "hugo import jekyll"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo import jekyll

[https://gohugo.io/commands/hugo_import_jekyll/](https://gohugo.io/commands/hugo_import_jekyll/)

## hugo import jekyll 

hugo import from Jekyll

### 概要

hugo import from Jekyll.

​	从 Jekyll 导入需要两个路径，例如： `hugo import jekyll jekyll_root_path target_path`.

```
hugo import jekyll [flags]
```

### 选项 

```
      --force   允许导入到非空目标目录中
  -h, --help    help for jekyll
```

### 从父命令继承的选项

```
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为 "config"）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略匹配给定 Glob 模式的模块路径下的任何 _vendor
      --log                        启用日志
      --logFile string             日志文件路径（如果设置，自动启用日志记录）
      --quiet                      安静模式下构建
  -s, --source string              从文件系统路径中相对读取文件
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    显示详细输出

```

### 另请参阅 

- [hugo import](https://gohugo.io/commands/hugo_import/) - 从其他站点生成器导入您的站点。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
