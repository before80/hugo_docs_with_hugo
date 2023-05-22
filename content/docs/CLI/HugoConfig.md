+++
title = "hugo config"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo config

[https://gohugo.io/commands/hugo_config/](https://gohugo.io/commands/hugo_config/)

## hugo config 

​	打印站点配置  

### 概要

​	打印站点配置，包括默认和自定义设置。

```
hugo config [flags]
```

### 选项 

```
      --clock string               set the clock used by Hugo, e.g. --clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         build environment
  -h, --help                       help for config
      --ignoreVendorPaths string   ignores any _vendor for module paths matching the given Glob pattern
  -s, --source string              filesystem path to read files relative from
      --themesDir string           filesystem path to themes directory
      
      --clock string               设置Hugo使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         构建环境
  -h, --help                       帮助配置
      --ignoreVendorPaths string   忽略任何与给定Glob模式匹配的模块路径的_vendor
  -s, --source string              相对于读取文件的文件系统路径
      --themesDir string           文件系统路径到主题目录
```

### 从父命令继承的选项

```
      --config string      配置文件（默认为hugo.yaml | json | toml）
      --configDir string   配置目录（默认值为“config”）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，则自动启用日志记录）
      --quiet              静默模式下构建
  -v, --verbose            详细输出
      --verboseLog         详细日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo构建您的站点 
- [hugo config mounts](https://gohugo.io/commands/hugo_config_mounts/) - 打印配置的文件挂载 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
