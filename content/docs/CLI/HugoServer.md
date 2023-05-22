+++
title = "hugo server"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo server

[https://gohugo.io/commands/hugo_server/](https://gohugo.io/commands/hugo_server/)

## hugo server 

​	一个高性能的 Web 服务器  

### 概要

​	Hugo 提供了自己的 Web 服务器，可以构建和提供站点。虽然 hugo server 性能很高，但它是一个选项有限的 Web 服务器。许多人在生产中运行它，但标准行为是在开发中使用它，（在生成中）使用更全面的服务器，例如 Nginx 或 Caddy。  

​	'hugo server' 将避免将渲染和提供的内容写入磁盘，而是将其存储在内存中。  

​	默认情况下，hugo 也会监视您所做的任何更改并自动重新构建站点。然后它将实时重新加载任何打开的浏览器页面并将最新内容推送到它们。由于大多数 Hugo 站点只需要几秒钟就可以构建完毕，因此您几乎可以立即保存和查看更改。

```
hugo server [flags]
```

### 选项 

```
	  --appendPort                 将端口附加到 baseURL 上（默认为 true）
  -b, --baseURL string             主机名（和路径）到根目录，例如 https://spf13.com/
      --bind string                服务器将绑定的接口（默认为 "127.0.0.1"）
  -D, --buildDrafts                包括标记为草稿的内容
  -E, --buildExpired               包括过期的内容
  -F, --buildFuture                包括发布日期在未来的内容
      --cacheDir string            缓存目录的文件系统路径。默认值：$TMPDIR/hugo_cache/
      --cleanDestinationDir        删除在静态目录中找不到的目标文件
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -c, --contentDir string          内容目录的文件系统路径
  -d, --destination string         写入文件的文件系统路径
      --disableBrowserError        不要在浏览器中显示构建错误
      --disableFastRender          启用完全重渲染以响应更改
      --disableKinds strings       禁用不同类型的页面（主页、RSS 等）
      --disableLiveReload          在重建时不启用实时浏览器重新加载
      --enableGitInfo              向页面添加 Git 修订版、日期、作者和 CODEOWNERS 信息
  -e, --environment string         构建环境
      --forceSyncStatic            当静态文件发生更改时复制所有文件。
      --gc                         启用后可在构建后运行一些清理任务（删除未使用的缓存文件）
  -h, --help                       server 的帮助信息
      --ignoreCache                忽略缓存目录
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径的 _vendor
  -l, --layoutDir string           布局目录的文件系统路径
      --liveReloadPort int         实时重新加载端口（例如 HTTPS 代理情况下的 443）（默认为 -1）
      --meminterval string         每隔一段时间轮询内存使用情况（需要 --memstats），有效的时间单位为 "ns"、"us"（或 "µs"）、"ms"、"s"、"m"、"h"。（默认为 "100ms"）
      --memstats string            将内存使用情况记录到这个文件中
      --minify                     缩小任何受支持的输出格式（HTML、XML 等）
      --navigateToChanged          在实时浏览器重新加载时导航到更改的内容文件
      --noBuildLock                不创建 .hugo_build.lock 文件
      --noChmod                    不同步文件的权限模式
      --noHTTPCache                防止 HTTP 缓存
      --noTimes                    不同步文件的修改时间
      --panicOnWarning             在第一个 WARNING 日志时 panic
      --poll string                将此设置为轮询间隔，例如 --poll 700ms，以使用基于轮询的方法来监视文件系统更改
  -p, --port int                   服务器将监听的端口（默认为 1313）
      --printI18nWarnings          打印缺少的翻译
      --printMemoryUsage           在一定间隔内将内存使用情况打印到屏幕上
      --printPathWarnings          打印有关重复目标路径等的警告
      --printUnusedTemplates       打印有关未使用模板的警告。
      --renderStaticToDisk         从磁盘提供静态文件，从内存提供动态文件
      --renderToDisk               从磁盘提供所有文件（默认情况下从内存提供）
  -s, --source string              相对于读取文件的文件系统路径
      --templateMetrics            显示有关模板执行的指标
      --templateMetricsHints       与 --templateMetrics 结合使用时计算一些改进提示
  -t, --theme strings              要使用的主题（位于 /themes/THEMENAME/ 中）
      --themesDir string           主题目录的文件系统路径
      --trace file                 将跟踪写入文件（通常不太有用）
  -w, --watch                      监视文件系统以进行更改，并根据需要重新创建（默认情况下为 true）
```

### 从父命令继承的选项

```
      --config string      配置文件（默认为 hugo.yaml|json|toml）
      --configDir string   配置目录（默认为 "config"）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，自动启用日志记录）
      --quiet              静默模式下构建
  -v, --verbose            冗长输出
      --verboseLog         冗长日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
