+++
title = "hugo deploy"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo deploy

[https://gohugo.io/commands/hugo_deploy/](https://gohugo.io/commands/hugo_deploy/)

## hugo deploy 

​	将您的站点部署到云提供商。  

### 概要

​	将您的站点部署到云提供商。  

​	请参阅 [https://gohugo.io/hosting-and-deployment/hugo-deploy/](https://gohugo.io/hosting-and-deployment/hugo-deploy/ ) 以获取详细的文档。

```
hugo deploy [flags]
```

### 选项 

```
	  --clock string               设置Hugo使用的时钟，例如--clock 2021-11-06T22:30:00.00+09:00
      --confirm                    在对目标进行更改之前要求确认
      --dryRun                     干况运行
  -e, --environment string         构建环境
      --force                      强制上传所有文件
  -h, --help                       deploy的帮助信息
      --ignoreVendorPaths string   忽略匹配给定Glob模式的模块路径中的任何_vendor
      --invalidateCDN              使部署目标中列出的CDN缓存失效（默认值为true）
      --maxDeletes int             要删除的文件的最大数量，或-1禁用（默认值为256）
      --workers int                传输文件的工作者数。（默认值为10）
  -s, --source string              从其中读取文件的文件系统路径
      --target string              部署目标中的目标部署在配置文件中；默认为第一个
      --themesDir string           主题目录的文件系统路径
```

### 从父命令继承的选项

```
	  --config string      配置文件（默认为hugo.yaml|json|toml）
      --configDir string   配置目录（默认为“config”）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，将自动启用日志记录）
      --quiet              静默模式下构建
  -v, --verbose            冗长输出
      --verboseLog         冗长日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - 构建您的站点

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
