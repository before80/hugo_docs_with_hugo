+++
title = "hugo new"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# hugo new

[https://gohugo.io/commands/hugo_new/](https://gohugo.io/commands/hugo_new/)

## hugo new 

​	为您的站点创建新内容

### 概要

​	创建一个新的内容文件并自动设置日期和标题。它将根据提供的路径猜测要创建哪种类型的文件。  

​	您还可以使用`-k KIND`指定种类。  

​	如果您的主题或站点中提供了原型模板，它们将被使用。  

​	请确保在站点的根目录中运行此命令。

```
hugo new [path] [flags]
```

### 选项 

```
  -b, --baseURL string             站点根目录的主机名（和路径），例如 https://spf13.com/
  -D, --buildDrafts                包括标记为草稿的内容
  -E, --buildExpired               包括过期内容
  -F, --buildFuture                包括发布日期在未来的内容
      --cacheDir string            缓存目录的文件系统路径。默认值：$TMPDIR/hugo_cache/。
      --cleanDestinationDir        删除目标文件夹中未在静态目录中找到的文件
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
  -c, --contentDir string          内容文件夹的文件系统路径
  -d, --destination string         写入文件的文件系统路径
      --disableKinds strings       禁用不同种类的页面（主页、RSS 等）
      --editor string              使用此编辑器编辑新内容（如果提供）
      --enableGitInfo              添加 Git 版本、日期、作者和 CODEOWNERS 信息到页面中
  -e, --environment string         构建环境
  -f, --force                      如果文件已经存在，则覆盖文件
      --forceSyncStatic            当静态文件发生更改时复制所有文件。
      --gc                         构建后启用以运行一些清理任务（删除未使用的缓存文件）
  -h, --help                       hugo new 的帮助信息
      --ignoreCache                忽略缓存目录
      --ignoreVendorPaths string   忽略匹配给定 Glob 模式的模块路径下的 _vendor。
  -k, --kind string                要创建的内容类型
  -l, --layoutDir string           布局文件夹的文件系统路径
      --minify                     缩小任何受支持的输出格式（HTML、XML 等）
      --noBuildLock                不创建 .hugo_build.lock 文件
      --noChmod                    不同步文件的权限模式
      --noTimes                    不同步文件的修改时间
      --panicOnWarning             在第一个 WARNING 日志上发生崩溃
      --poll string                将其设置为轮询间隔，例如 --poll 700ms，使其使用基于轮询的方法来监视文件系统更改
      --printI18nWarnings          打印缺少的翻译
      --printMemoryUsage           定期在屏幕上打印内存使用情况
      --printPathWarnings          打印有关重复目标路径的警告等
      --printUnusedTemplates       打印未使用模板的警告。
  -s, --source string              从中读取文件的文件系统路径
      --templateMetrics            显示有关模板执行的指标
      --templateMetricsHints       与 --templateMetrics 结合使用时，计算某些改进提示
  -t, --theme strings              要使用的主题（位于 /themes/THEMENAME/ 中）
      --themesDir string           主题文件夹的文件系统路径
      --trace file                 将跟踪写入文件（通常不会有用）
```

### 从父命令继承的选项

```
      --config string      配置文件（默认为 hugo.yaml|json|toml）
      --configDir string   配置目录（默认为 "config"）
      --debug              调试输出
      --log                启用日志记录
      --logFile string     日志文件路径（如果设置，自动启用日志记录）
      --quiet              安静模式下构建
  -v, --verbose            冗长的输出
      --verboseLog         冗长的日志记录
```

### 另请参阅 

- [hugo](https://gohugo.io/commands/hugo/) - hugo 构建您的站点
- [hugo new site](https://gohugo.io/commands/hugo_new_site/) -  创建一个新的站点（框架 （skeleton））
- [hugo new theme](https://gohugo.io/commands/hugo_new_theme/) - 创建一个新的主题

## 另请参阅

- [hugo completion](https://gohugo.io/commands/hugo_completion/)
- [hugo completion bash](https://gohugo.io/commands/hugo_completion_bash/)
- [hugo completion fish](https://gohugo.io/commands/hugo_completion_fish/)
- [hugo completion powershell](https://gohugo.io/commands/hugo_completion_powershell/)
- [hugo completion zsh](https://gohugo.io/commands/hugo_completion_zsh/)
