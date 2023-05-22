+++
title = "hugo gen chromastyles"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo gen chromastyles

[https://gohugo.io/commands/hugo_gen_chromastyles/](https://gohugo.io/commands/hugo_gen_chromastyles/)

## hugo gen chromastyles 

​	为 Chroma 代码高亮器生成 CSS 样式表  

### 概要

​	为给定样式的 Chroma 代码高亮器生成 CSS 样式表。如果在配置中禁用了 `markup.highlight.noClasses`，则需要此样式表。  

​	请参阅 [https://xyproto.github.io/splash/docs/all.html](https://xyproto.github.io/splash/docs/all.html ) 以预览可用的样式。

```
hugo gen chromastyles [flags]
```

### 选项 

```
	-h, --help                    帮助信息
        --highlightStyle string   用于突出显示行的样式（请参阅 https://github.com/alecthomas/chroma）（默认值为“bg:#ffffcc”）
        --linesStyle string       用于行号的样式（请参阅 https://github.com/alecthomas/chroma）
        --style string            高亮器样式（请参阅 https://xyproto.github.io/splash/docs/）（默认值为“friendly”）
```

### 从父命令继承的选项

```
	  --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为“config”）
      --debug                      调试输出
  -e, --environment string         构建环境
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径中的任何 _vendor
      --log                        启用日志记录
      --logFile string             日志文件路径（如果设置，将自动启用日志记录）
      --quiet                      在安静模式下构建
  -s, --source string              从文件系统路径读取相对文件
      --themesDir string           主题目录的文件系统路径
  -v, --verbose                    冗长输出
      --verboseLog                 冗长的日志记录
```

### 另请参阅 

- [hugo gen](https://gohugo.io/commands/hugo_gen/) - 一个包含多个有用生成器的集合。 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
