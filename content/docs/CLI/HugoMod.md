+++
title = "hugo mod"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo mod

[https://gohugo.io/commands/hugo_mod/](https://gohugo.io/commands/hugo_mod/)

## hugo mod 

​	各种 Hugo 模块的辅助工具。

### 概要

​	提供各种辅助工具，以帮助管理项目依赖图中的模块。

​	大多数操作需要在您的系统上安装 Go 版本（>= Go 1.12）和相关的版本控制系统客户端（通常是 Git）。如果您仅在 /themes 内操作模块或通过 "hugo mod vendor" 将它们标记为供应商，则不需要安装它们。

​	这里的大多数操作需要在您的系统上安装了Go版本（>= Go 1.12）和相关的VCS客户端（通常是Git）。如果您只操作/themes中的模块，或者通过 "hugo mod vendor" 将它们打包到_vendor目录，那么不需要这些依赖。  

​	请注意，Hugo将始终首先解析站点配置中定义的组件，这些组件由_vendor目录（如果没有提供`-ignoreVendorPaths`标志）、Go模块或主题目录内的文件夹提供，按照此顺序解析。

​	有关更多信息，请参见 [https://gohugo.io/hugo-modules/](https://gohugo.io/hugo-modules/)。

### 选项 

```
  -b, --baseURL string             根目录的主机名（和路径），例如 https://spf13.com/
  -D, --buildDrafts                包括被标记为草稿的内容
  -E, --buildExpired               包括已过期的内容
  -F, --buildFuture                包括未来发布日期的内容
      --cacheDir string            缓存目录的文件系统路径。默认为：$TMPDIR/hugo_cache/
      --cleanDestinationDir        删除目标中未在静态目录中找到的文件
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -c, --contentDir string          内容目录的文件系统路径
  -d, --destination string         要写入文件的文件系统路径
      --disableKinds strings       禁用不同类型的页面（主页、RSS 等）
      --enableGitInfo              将 Git 版本、日期、作者和 CODEOWNERS 信息添加到页面中
  -e, --environment string         构建环境
      --forceSyncStatic            当静态文件更改时复制所有文件。
      --gc                         启用以运行一些清理任务（删除未使用的缓存文件）。
  -h, --help                       查看 mod 帮助
      --ignoreCache                忽略缓存目录
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的任何 _vendor
  -l, --layoutDir string           布局目录的文件系统路径
      --minify                     最小化任何支持的输出格式（HTML、XML 等）
      --noBuildLock                不创建 .hugo_build.lock 文件
      --noChmod                    不同步文件的权限模式
      --noTimes                    不同步文件的修改时间
      --panicOnWarning             在第一个 WARNING 日志上引发 panic
      --poll string                将其设置为轮询

```

### 从父命令继承的选项

```
	  --config string      配置文件（默认为hugo.yaml|json|toml）
      --configDir string   配置目录（默认为 "config"）
      --debug              调试输出
      --log                启用日志
      --logFile string     日志文件路径（如果设置，自动启用日志）
      --quiet              安静模式构建
  -v, --verbose            详细输出
      --verboseLog         详细日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点
- [hugo mod clean](https://gohugo.io/commands/hugo_mod_clean/) - 删除当前项目的Hugo模块缓存。 
- [hugo mod get](https://gohugo.io/commands/hugo_mod_get/) - 解析您当前的Hugo项目的依赖项。 
- [hugo mod graph](https://gohugo.io/commands/hugo_mod_graph/) - 打印模块依赖关系图表。 
- [hugo mod init](https://gohugo.io/commands/hugo_mod_init/) - 将此项目初始化为Hugo模块。 
- [hugo mod npm](https://gohugo.io/commands/hugo_mod_npm/) - 各种npm助手。 
- [hugo mod tidy](https://gohugo.io/commands/hugo_mod_tidy/) - 删除go.mod和go.sum中未使用的条目。 
- [hugo mod vendor](https://gohugo.io/commands/hugo_mod_vendor/) - 将所有模块依赖项打包到_vendor目录中。 
- [hugo mod verify](https://gohugo.io/commands/hugo_mod_verify/) - 校验依赖关系。 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
