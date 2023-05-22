+++
title = "hugo import"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo import

[https://gohugo.io/commands/hugo_import/](https://gohugo.io/commands/hugo_import/)

## hugo import 

​	从其他站点生成器导入您的站点。  

### 概要

​	从其他站点生成器（如Jekyll）导入您的站点。  

​	导入需要一个子命令，例如  `hugo import jekyll jekyll_root_path target_path` 。  

### 选项 

```
  -h, --help   help for import
```

### 从父命令继承的选项

```
	 --clock string               设置Hugo使用的时钟，例如：--clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为hugo.yaml | json | toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定Glob模式匹配的模块路径的任何_vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置了，则自动启用日志记录）
      --quiet                      在静默模式下构建
  -s, --source string              用于读取文件的文件系统路径
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    冗长输出
      --verboseLog                 冗长日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点
- [hugo import jekyll](https://gohugo.io/commands/hugo_import_jekyll/) - hugo import from Jekyll

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
