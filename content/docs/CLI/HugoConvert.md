+++
title = "hugo convert"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo convert

[https://gohugo.io/commands/hugo_convert/](https://gohugo.io/commands/hugo_convert/)

## hugo convert 

​	将您的内容转换为不同的格式  

### 概要

​	将您的内容（例如前置元数据）转换为不同的格式。  

​	有关更多信息，请参见转换的子命令 toJSON、toTOML 和 toYAML。  

### 选项 

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -e, --environment string         构建环境
  -h, --help                       convert 的帮助信息
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的任何 _vendor
  -o, --output string              要将文件写入的文件系统路径
  -s, --source string              从中读取文件的文件系统路径相对路径
      --themesDir string           主题目录的文件系统路径
      --unsafe                     启用不安全的操作，请先备份
```

### 从父命令继承的选项

```
	  --config string      配置文件（默认为 hugo.yaml|json|toml）
      --configDir string   配置目录（默认为“config”）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，将自动启用日志记录）
      --quiet              安静模式构建
  -v, --verbose            详细输出
      --verboseLog         详细日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点 
- [hugo convert toJSON](https://gohugo.io/commands/hugo_convert_tojson/) - 将前置元数据转换为 JSON 
- [hugo convert toTOML](https://gohugo.io/commands/hugo_convert_totoml/) - 将前置元数据转换为 TOML 
- [hugo convert toYAML](https://gohugo.io/commands/hugo_convert_toyaml/) - 将前置元数据转换为 YAML 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
