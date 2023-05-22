+++
title = "hugo"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo

[https://gohugo.io/commands/hugo/](https://gohugo.io/commands/hugo/)



## hugo 

​	hugo 构建您的站点  

### 概要

​	hugo 是主要命令，用于构建您的Hugo站点。  

​	Hugo 是一个用 Go 语言编写的快速且灵活的静态站点生成器，由 spf13 和朋友们倾情打造。  

​	完整文档请访问 https://gohugo.io/。	

```
hugo [flags]
```

### 选项 

```
  -b, --baseURL string             主机名（和根路径），例如https://spf13.com/
  -D, --buildDrafts                包含标记为草稿的内容
  -E, --buildExpired               包含已过期的内容
  -F, --buildFuture                包含将来发布日期的内容
      --cacheDir string            缓存目录的文件系统路径。默认值：$TMPDIR/hugo_cache/
      --cleanDestinationDir        从目标目录中删除未在静态目录中找到的文件
      --clock string               设置Hugo使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件（默认为 hugo.yaml|json|toml）
      --configDir string           配置目录（默认为 "config"）
  -c, --contentDir string          内容目录的文件系统路径
      --debug                      调试输出
  -d, --destination string         写入文件的文件系统路径
      --disableKinds strings       禁用不同类型的页面（首页、RSS 等）
      --enableGitInfo              将 Git 修订、日期、作者和 CODEOWNERS 信息添加到页面
  -e, --environment string         构建环境
      --forceSyncStatic            当静态内容发生更改时，复制所有文件。
      --gc                         启用在构建后运行一些清理任务（删除未使用的缓存文件）
  -h, --help                       hugo 的帮助
      --ignoreCache                忽略缓存目录
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径中的任何 _vendor
  -l, --layoutDir string           布局目录的文件系统路径
      --log                        启用日志
      --logFile string             日志文件路径（如果设置，日志自动启用）
      --minify                     最小化任何支持的输出格式（HTML、XML 等）
      --noBuildLock                不创建.hugo_build.lock文件
      --noChmod                    不同步文件的权限模式
      --noTimes                    不同步文件的修改时间
      --panicOnWarning             在第一个警告日志上发生恐慌
      --poll string                将其设置为轮询间隔，例如 --poll 700ms，以使用基于轮询的方法来监视文件系统更改
      --printI18nWarnings          打印缺失的翻译
      --printMemoryUsage           在间隔期内将内存使用情况打印到屏幕上
      --printPathWarnings          打印关于重复目标路径等的警告
      --printUnusedTemplates       打印未使用的模板的警告。
      --quiet                      安静模式构建
      --renderToMemory             将渲染结果存储到内存中（仅对基准测试有用）
  -s, --source string              从中读取文件的文件系统路径
      --templateMetrics            显示关于模板执行的指标
      --templateMetricsHints       在与 --templateMetrics 结合使用时，计算一些改进提示
  -t, --theme strings              要使用的主题（位于/themes/THEMENAME/）
      --themesDir string           主题目录的文件系统路径
      --trace file                 将跟踪写入文件（通常没有用处）
  -v, --verbose                    详细输出
      --verboseLog                 详细日志
  -w, --watch                      观察文件系统变化，并根据需要重新创建
```

### 另请参阅 

- [hugo completion](https://gohugo.io/commands/hugo_completion/) - 为指定的 shell 生成自动补全脚本 
- [hugo config](https://gohugo.io/commands/hugo_config/) - 打印站点配置 
- [hugo convert](https://gohugo.io/commands/hugo_convert/) - 将您的内容转换为不同格式 
- [hugo deploy](https://gohugo.io/commands/hugo_deploy/) - 将您的站点部署到云提供商。 
- [hugo env](https://gohugo.io/commands/hugo_env/) - 打印 Hugo 版本和环境信息 
- [hugo gen](https://gohugo.io/commands/hugo_gen/) - 多个有用的生成器的集合。 
- [hugo import](https://gohugo.io/commands/hugo_import/) - 从其他来源导入您的站点。 
- [hugo list](https://gohugo.io/commands/hugo_list/) - 列出各种类型的内容 
- [hugo mod](https://gohugo.io/commands/hugo_mod/) - 各种 Hugo 模块助手。 
- [hugo new](https://gohugo.io/commands/hugo_new/) - 为您的站点创建新内容 
- [hugo server](https://gohugo.io/commands/hugo_server/) - 一个高性能的网络服务器 
- [hugo version](https://gohugo.io/commands/hugo_version/) - 打印 Hugo 的版本号 

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
