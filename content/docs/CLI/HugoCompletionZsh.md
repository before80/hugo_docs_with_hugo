+++
title = "hugo completion zsh"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo completion zsh

[https://gohugo.io/commands/hugo_completion_zsh/](https://gohugo.io/commands/hugo_completion_zsh/)

## hugo completion zsh 

​	生成zsh shell的自动补全脚本。  

### 概要

​	生成zsh shell的自动补全脚本。  

​	如果您的环境中没有启用 shell 自动补全，您需要启用它。您可以执行以下命令：

```
echo "autoload -U compinit; compinit" >> ~/.zshrc
```

​	为了在当前的 shell 会话中载入自动补全：

```
source <(hugo completion zsh); compdef _hugo hugo
```

​	要为每个新会话加载自动补全，请执行以下操作一次：

#### Linux: 

```
hugo completion zsh > "${fpath[1]}/_hugo"
```

#### macOS: 

```
hugo completion zsh > $(brew --prefix)/share/zsh/site-functions/_hugo
```

​	您需要启动一个新的shell才能使此设置生效。

```
hugo completion zsh [flags]
```

### 选项 

```
  -h, --help              help for zsh
      --no-descriptions   禁用completion说明
```

### 从父命令继承的选项

```
	 --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
     --config string              配置文件 (默认为 hugo.yaml|json|toml)
     --configDir string           配置目录 (默认 "config")
     --debug                      调试输出
 -e, --environment string         构建环境
     --ignoreVendorPaths string   忽略任何与给定 Glob 模式匹配的模块路径的 _vendor
     --log                        启用日志记录
     --logFile string             日志文件路径（如果设置，自动启用日志记录）
     --quiet                      安静模式下构建
 -s, --source string              文件系统路径，从中读取相对文件
     --themesDir string           主题目录的文件系统路径
 -v, --verbose                    冗长的输出
     --verboseLog                 冗长的日志记录
```

### 另请参阅 

- [hugo completion](https://gohugo.io/commands/hugo_completion/) - 为指定的shell生成自动完成脚本 

## 另请参阅

- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo config](https://gohugo.io/commands/hugo_config/)
