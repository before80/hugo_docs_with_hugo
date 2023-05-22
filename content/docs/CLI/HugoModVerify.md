+++
title = "hugo mod verify"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod verify

[https://gohugo.io/commands/hugo_mod_verify/](https://gohugo.io/commands/hugo_mod_verify/)

## hugo mod verify 

​	验证依赖项。

### 概要

​	verify 检查当前模块的依赖项是否已被下载到本地源缓存中，在下载后是否已被修改。

```
hugo mod verify [flags]
```

### 选项 

```
      --clean   如果验证失败则删除依赖项的模块缓存
  -h, --help    help for verify
```

### 从父命令继承的选项

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为 "config"）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的任何 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，则自动启用日志记录）
      --quiet                      静默模式下进行构建
  -s, --source string              读取相对文件的文件系统路径
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    详细输出
      --verboseLog                 详细日志记录
```

### 另请参阅 

- [hugo mod](https://gohugo.io/commands/hugo_mod/) - 各种 Hugo 模块助手。

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
