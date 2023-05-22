+++
title = "配置 Hugo"
weight = 4
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Configure Hugo - 配置 Hugo 

[https://gohugo.io/getting-started/configuration/](https://gohugo.io/getting-started/configuration/)

​	如何配置您的 Hugo 站点。 

## 配置文件 

​	Hugo 使用 `config.toml`、`config.yaml` 或 `config.json`（如果在站点根目录中找到）作为默认的站点配置文件。

​	用户可以使用命令行 `--config` 开关选择覆盖默认设置的一个或多个站点配置文件。

例如：

```txt
hugo --config debugconfig.toml
hugo --config a.toml,b.toml,c.toml
```

> ​	可以将多个站点配置文件指定为逗号分隔的字符串传递给 `--config` 开关。
>

## hugo.toml vs config.toml 

​	在 Hugo 0.110.0 中，我们将默认的配置基础文件名更改为 `hugo`，例如 `hugo.toml`。我们仍会查找 `config.toml` 等文件，但我们建议您最终将其重命名（但如果您想支持旧版本的 Hugo，则需要等待）。我们这样做的主要原因是为了让代码编辑器和构建工具更容易识别这是 Hugo 的配置文件和项目。

[v0.110.0 新功能 ](https://github.com/gohugoio/hugo/releases/tag/v0.110.0)

## 配置目录 

​	除了使用单个站点配置文件外，您还可以使用 `configDir` 目录（默认为 `config/`）来维护更易于组织和特定于环境的设置。

- 每个文件都代表一个配置根对象，例如 `params.toml` 代表 `[Params]`，`menu(s).toml` 代表 `[Menu]`，`languages.toml` 代表 `[Languages]` 等等… 
- 每个文件的内容必须是顶级的，例如：

config.

=== "yaml"

    ```yaml
    Params:
      foo: bar
    ```

=== "toml"

    ```toml
    [Params]
      foo = 'bar'
    ```

=== "json"

    ```json
    {
        "Params": {
              "foo": "bar"
        }
    }
    ```



params.

=== "yaml"

    ```yaml
    foo: bar
    ```

=== "toml"

    ```toml
    foo = 'bar'
    ```

=== "json"

    ```json
    {
       "foo": "bar"
    }
    ```



- 每个目录保存了一组文件，包含特定环境的设置。
- 文件可以本地化，变成特定语言。

```txt
├── config
│   ├── _default
│   │   ├── config.toml
│   │   ├── languages.toml
│   │   ├── menus.en.toml
│   │   ├── menus.zh.toml
│   │   └── params.toml
│   ├── production
│   │   ├── config.toml
│   │   └── params.toml
│   └── staging
│       ├── config.toml
│       └── params.toml
```

​	考虑上述结构，在运行`hugo --environment staging`命令时，Hugo将使用`config/_default`中的所有设置，并在其上合并`staging`的设置。

​	让我们举个例子来更好地理解这个过程。假设您的站点使用Google Analytics。这要求您在`config.toml`中指定`googleAnalytics = "G-XXXXXXXX"`。现在考虑以下场景：

- 您不希望在开发中加载分析代码，即在`localhost`上。 
- 您想为生产和staging环境使用不同的googleAnalytics ID： 
  - 生产环境的`G-PPPPPPPP` 
  - staging环境的`G-SSSSSSSS` 

​	考虑上述情况，您需要如何配置您的`config.toml`文件：

1. 在`_default/config.toml`中，您根本不需要提及`googleAnalytics`参数。这可以确保在您运行`hugo server`时，即在您的开发服务器上不加载Google Analytics代码。这是因为，当您运行`hugo server`时，默认情况下Hugo设置`Environment=development`，它使用`_default`文件夹中的配置文件。

2. 在`production/config.toml`中，您只需要有一行：

   `googleAnalytics = "G-PPPPPPPP"`

   您不需要在此配置文件中再次提及所有其他参数，如`title`、`baseURL`、`theme`等。您只需要提及那些不同或新的生产环境参数。这是由于Hugo将在`_default/config.toml`之上合并此参数。现在，当您运行`hugo`（build命令）时，默认情况下hugo设置`Environment=production`，因此`G-PPPPPPPP`分析代码将存在于您的生产站点中。

3. 同样，在`staging/config.toml`中，您只需要有一行：

   `googleAnalytics = "G-SSSSSSSS"`

   现在，您需要告诉Hugo您正在使用staging环境。因此，您的构建命令应该是`hugo --environment staging`，这将在您的staging站点中加载`G-SSSSSSSS`分析代码。

>
> ​	默认环境是`hugo server`下的`development`和hugo下的`production`。
>

## 合并主题配置 

​	`_merge` 的配置值可以是以下之一：

- none

  不合并。 

- shallow

  仅添加新键的值。 

- deep

  添加新键的值，合并现有键的值。

​	请注意，您不需要像下面的默认设置那样冗长；如果未设置，则会继承更高的`_merge`值。

config.

=== "yaml"

    ```yaml
    build:
      _merge: none
    caches:
      _merge: none
    cascade:
      _merge: none
    frontmatter:
      _merge: none
    imaging:
      _merge: none
    languages:
      _merge: none
      en:
        _merge: none
        menus:
          _merge: shallow
        params:
          _merge: deep
    markup:
      _merge: none
    mediatypes:
      _merge: shallow
    menus:
      _merge: shallow
    minify:
      _merge: none
    module:
      _merge: none
    outputformats:
      _merge: shallow
    params:
      _merge: deep
    permalinks:
      _merge: none
    privacy:
      _merge: none
    related:
      _merge: none
    security:
      _merge: none
    sitemap:
      _merge: none
    taxonomies:
      _merge: none
    ```

=== "toml"

    ```toml
    [build]
      _merge = 'none'
    [caches]
      _merge = 'none'
    [cascade]
      _merge = 'none'
    [frontmatter]
      _merge = 'none'
    [imaging]
      _merge = 'none'
    [languages]
      _merge = 'none'
      [languages.en]
        _merge = 'none'
        [languages.en.menus]
          _merge = 'shallow'
        [languages.en.params]
          _merge = 'deep'
    [markup]
      _merge = 'none'
    [mediatypes]
      _merge = 'shallow'
    [menus]
      _merge = 'shallow'
    [minify]
      _merge = 'none'
    [module]
      _merge = 'none'
    [outputformats]
      _merge = 'shallow'
    [params]
      _merge = 'deep'
    [permalinks]
      _merge = 'none'
    [privacy]
      _merge = 'none'
    [related]
      _merge = 'none'
    [security]
      _merge = 'none'
    [sitemap]
      _merge = 'none'
    [taxonomies]
      _merge = 'none'
    ```

=== "json"

    ```json
    {
       "build": {
          "_merge": "none"
       },
       "caches": {
          "_merge": "none"
       },
       "cascade": {
          "_merge": "none"
       },
       "frontmatter": {
          "_merge": "none"
       },
       "imaging": {
          "_merge": "none"
       },
       "languages": {
          "_merge": "none",
          "en": {
             "_merge": "none",
             "menus": {
                "_merge": "shallow"
             },
             "params": {
                "_merge": "deep"
             }
          }
       },
       "markup": {
          "_merge": "none"
       },
       "mediatypes": {
          "_merge": "shallow"
       },
       "menus": {
          "_merge": "shallow"
       },
       "minify": {
          "_merge": "none"
       },
       "module": {
          "_merge": "none"
       },
       "outputformats": {
          "_merge": "shallow"
       },
       "params": {
          "_merge": "deep"
       },
       "permalinks": {
          "_merge": "none"
       },
       "privacy": {
          "_merge": "none"
       },
       "related": {
          "_merge": "none"
       },
       "security": {
          "_merge": "none"
       },
       "sitemap": {
          "_merge": "none"
       },
       "taxonomies": {
          "_merge": "none"
       }
    }
    ```



## 所有配置设置 

​	以下是Hugo定义的变量的完整列表。用户可以选择在其站点配置文件中覆盖这些值。

### archetypeDir 

​	默认值："archetypes"

​	Hugo查找原型文件（内容模板）的目录。另请参阅[模块挂载配置](https://gohugo.io/hugo-modules/configuration/#module-config-mounts)，以了解配置此目录的另一种替代方式（从Hugo 0.56开始）。

### assetDir 

​	默认值："assets"

​	Hugo查找[Hugo Pipes](https://gohugo.io/hugo-pipes/)中使用的资产文件的目录。另请参阅[模块挂载配置](https://gohugo.io/hugo-modules/configuration/#module-config-mounts)，以了解配置此目录的另一种替代方式（从Hugo 0.56开始）。

### baseURL 

​	您发布站点的绝对 URL（协议、主机、路径和尾随斜杠），例如 `https://www.example.org/docs/`。

### build 

​	请参阅[配置构建](https://gohugo.io/getting-started/configuration/#configure-build)

### buildDrafts (false) 

​	默认值：false

​	在构建时包括草稿。

### buildExpired 

​	默认值：false

​	包括已过期的内容。

### buildFuture 

​	默认值：false

​	包括发布日期在未来的内容。

### caches 

​	请参阅[配置文件缓存](https://gohugo.io/getting-started/configuration/#configure-file-caches)

### cascade 

​	将默认配置值（正面）传递到内容树中的页面。站点配置中的选项与页面前置元数据相同，请参阅[前置元数据层叠](https://gohugo.io/content-management/front-matter#front-matter-cascade)。

### canonifyURLs 

​	默认值：false

​	启用将相对URL转换为绝对URL。

### cleanDestinationDir 

​	默认值：false

​	在构建时，从目标中删除在static 目录中找不到的文件。

### contentDir 

​	默认值："content"

​	Hugo读取内容文件的目录。也可以参考[模块安装配置](https://gohugo.io/hugo-modules/configuration/#module-config-mounts)的另一种方式来配置此目录（从Hugo 0.56开始）。

### copyright 

​	默认值：""

​	站点的版权声明，通常显示在页脚上。

### dataDir 

​	默认值："data"

​	Hugo读取数据文件的目录。也可以参考[模块安装配置](https://gohugo.io/hugo-modules/configuration/#module-config-mounts)的另一种方式来配置此目录（从Hugo 0.56开始）。

### defaultContentLanguage <-

​	默认值："en"

​	没有语言标识的内容将默认为此语言。

### defaultContentLanguageInSubdir 

​	默认值：false

​	在子目录中呈现默认的内容语言，例如`content/en/`。站点根目录`/`将重定向到`/en/`。

### disableAliases 

​	默认值：false

​	禁用别名重定向的生成。请注意，即使设置了`disableAliases`，别名本身仍将保留在页面上。这样做的动机是能够在`.htaccess`、Netlify `_redirects`文件或类似的输出格式中使用301重定向。

### disableHugoGeneratorInject 

​	默认值：false

​	Hugo默认情况下**仅在主页**的HTML头中插入一个生成器元标记。您可以关闭它，但我们真的很希望您不要这样做，因为这是观察Hugo的受欢迎程度的好方法。

### disableKinds 

​	默认值：[]

​	启用禁用指定类型的所有页面。在此列表中允许的值为：`"page"`、`"home"`、`"section"`、`"taxonomy"`、`"term"`、`"RSS"`、`"sitemap"`、`"robotsTXT"`、`"404"`。

### disableLiveReload 

​	默认值：false

​	禁用浏览器窗口的自动实时重新加载。

### disablePathToLower 

​	默认值：false

​	不要将url/path转换为小写。

### enableEmoji <-

​	默认值：false

​	为页面内容启用表情符号支持；参见[Emoji备忘表](https://www.webpagefx.com/tools/emoji-cheat-sheet/)。

### enableGitInfo <-

​	默认值：false

​	为每个页面启用`.GitInfo`对象（如果Hugo站点已经通过Git进行版本控制）。这将使用每个内容文件的最后git提交日期来更新每个页面的`Lastmod`参数。

### enableInlineShortcodes 

​	默认值：false

​	启用内联shortcode 支持。参见[内联shortcode](https://gohugo.io/templates/shortcode-templates/#inline-shortcodes) 。

### enableMissingTranslationPlaceholders 

​	默认值：false

​	如果缺少翻译，则显示占位符，而不是默认值或空字符串。

### enableRobotsTXT <-

​	默认值：false

​	启用`robots.txt`文件的生成。

### frontmatter 

​	请参阅[前置元数据配置](https://gohugo.io/getting-started/configuration/#configure-front-matter)。

### googleAnalytics 

​	默认值：""

​	Google Analytics 跟踪 ID。

### hasCJKLanguage <-

​	默认值：false

​	如果为 true，则自动检测内容中的中文/日文/韩文语言。这将使得 `.Summary` 和 `.WordCount` 在 CJK 语言中正确工作。

### imaging 

​	请参阅[图像处理配置](https://gohugo.io/content-management/image-processing/#imaging-configuration)。

### languageCode 

​	默认值：""

​	由 [RFC 5646](https://datatracker.ietf.org/doc/html/rfc5646) 定义的语言标签。此值用于填充：

- 内部 [RSS 模板](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/rss.xml)中的 `<language>` 元素 
- 内部[别名模板](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/alias.html)中 `<html>` 元素的 `lang` 属性

### languages 

​	请参阅[配置语言](https://gohugo.io/content-management/multilingual/#configure-languages)。

### disableLanguages 

​	请参阅[禁用语言](https://gohugo.io/content-management/multilingual/#disable-a-language)。

### markup 

​	请参阅[配置标记](https://gohugo.io/getting-started/configuration-markup)。

### mediaTypes 

​	请参阅[配置媒体类型](https://gohugo.io/templates/output-formats/#media-types)。

### menus <-

​	请参阅[菜单](https://gohugo.io/content-management/menus/#define-in-site-configuration)。

### minify 

​	请参阅[配置 Minify](https://gohugo.io/getting-started/configuration/#configure-minify)。

### module 

​	模块配置，请参阅[模块配置](https://gohugo.io/hugo-modules/configuration/)。

### newContentEditor 

​	默认值：""

​	创建新内容时要使用的编辑器。

### noChmod 

​	默认值：false

​	不同步文件的权限模式。

### noTimes 

​	默认值：false

​	不同步文件的修改时间。

### outputFormats 

​	请参阅[配置输出格式](https://gohugo.io/getting-started/configuration/#configure-additional-output-formats)。

### paginate <-

​	默认值：10

​	[分页](https://gohugo.io/templates/pagination/)中每页的默认元素数。

### paginatePath 

​	默认值："page"

​	在分页期间使用的路径元素（`https://example.com/page/2`）。

### permalinks 

​	请参阅[内容管理](https://gohugo.io/content-management/urls/#permalinks)。

### pluralizeListTitles 

​	默认值：true

​	在列表中使用复数形式的标题。

### publishDir 

​	默认值："public"

​	Hugo将生成的最终静态站点（HTML文件等）写入的目录。

### related 

​	请参阅相关内容（[Related Content](https://gohugo.io/content-management/related/#configure-related-content)）。

### relativeURLs 

​	默认值：false

​	启用此选项可使所有相对URL相对于内容根目录。请注意，这不会影响绝对URL。

### refLinksErrorLevel 

​	默认值："ERROR"

​	使用`ref`或`relref`解析页面链接时，如果无法解析链接，将以此日志级别记录。有效值为`ERROR`（默认值）或`WARNING`。任何`ERROR`将导致构建失败（`exit -1`）。

### refLinksNotFoundURL 

​	在`ref`或`relref`中找不到页面引用时要使用的URL占位符。按原样使用。

### removePathAccents 

​	默认值：false

​	从内容路径中的[组合字符](https://en.wikipedia.org/wiki/Precomposed_character)中删除[非间隔标记](https://www.compart.com/en/unicode/category/Mn)。

```text
content/post/hügó.md --> https://example.org/post/hugo/
```

### rssLimit 

​	默认值：-1（无限制）

​	RSS feed中的最大项目数。

### sectionPagesMenu 

​	请参阅菜单（[Menus](https://gohugo.io/content-management/menus/#define-in-site-configuration)）。

### security 

​	请参阅安全策略（[Security Policy](https://gohugo.io/about/security-model/#security-policy)）。

### sitemap 

​	默认[站点地图配置](https://gohugo.io/templates/sitemap-template/#configuration)。

### summaryLength 

​	默认值：70

​	在`.Summary`中显示的文本长度（以单词计算）。

### taxonomies 

​	请参阅分类（[Configure Taxonomies](https://gohugo.io/content-management/taxonomies#configure-taxonomies)）。

### theme 

​	请参阅模块配置（[Module Config](https://gohugo.io/hugo-modules/configuration/#module-config-imports)）以了解如何导入主题。

### themesDir 

​	默认值："themes"

​	Hugo从中读取主题的目录。

### timeout 

​	默认值："30s"

​	生成页面内容的超时时间，以[持续时间](https://pkg.go.dev/time#Duration)或毫秒表示。注意：这用于退出递归内容生成。如果页面生成较慢（例如因为它们需要大量的图像处理或依赖于远程内容），则可能需要提高此限制。

### timeZone <-

​	用于解析前置元数据日期（不带此信息）和[`time` function](https://gohugo.io/functions/time/)的时区（或位置），例如`Europe/Oslo`。有效值列表可能因系统而异，但应包括`UTC`、`Local`和[IANA时区数据库](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)中的任何位置。

### title 

​	站点标题。

### titleCaseStyle 

​	默认值："AP"

​	请参阅配置标题大小写（[Configure Title Case](https://gohugo.io/getting-started/configuration/#configure-title-case)）。

### uglyURLs 

​	默认值：false

​	启用时，将创建形式为`/filename.html`而不是`/filename/`的URL。

### watch 

​	默认值：false

​	监视文件系统以进行更改，并根据需要重新创建。

> ​	如果您在`*nix`机器上开发您的站点，这是一个方便的从命令行查找配置选项的快捷方式：
>
> ```bash
> cd ~/sites/yourhugosite
> hugo config | grep emoji
> ```
>
> 显示输出如下：
>
> ```txt
> enableemoji: true
> ```
>
> 

## 配置构建 -> [build]

​	`build`配置部分包含全局构建相关的配置选项。

config.

=== "yaml"

    ```yaml
    build:
      noJSConfigInAssets: false
      useResourceCacheWhen: fallback
      writeStats: false
    ```

=== "toml"

    ```toml
    [build]
      noJSConfigInAssets = false
      useResourceCacheWhen = 'fallback'
      writeStats = false
    ```

=== "json"

    ```json
    {
       "build": {
          "noJSConfigInAssets": false,
          "useResourceCacheWhen": "fallback",
          "writeStats": false
       }
    }
    ```



- useResourceCacheWhen

  决定在 PostCSS 和 ToCSS 中何时使用 `/resources/_gen` 中的缓存资源。有效值为 `never`、`always` 和 `fallback`。最后一个值表示如果 PostCSS/extended版本不可用，则尝试使用缓存。

- writeStats

  启用后，将在项目根目录下写入一个名为 `hugo_stats.json` 的文件，其中包含有关构建的一些汇总数据，例如已发布的 HTML 实体列表，可用于进行 [CSS pruning](https://gohugo.io/hugo-pipes/postprocess/#css-purging-with-postcss)。如果您仅在生产构建中使用此功能，则应考虑将其放在 [config/production](https://gohugo.io/getting-started/configuration/#configuration-directory) 下面。值得一提的是，由于部分服务器构建的本质，当您添加或更改 HTML 实体时，将添加新的 HTML 实体，但旧值不会在您重启服务器或运行常规的 `hugo` 构建之前被删除。

请注意，这是清除未使用的 CSS 的主要用例；它专为速度而建，可能会出现误报（例如，检测到不是 HTML 元素的 HTML 元素）。

- noJSConfigInAssets

  关闭在 `/assets` 文件夹中写入一个 `jsconfig.json`，其中包含来自运行 [js.Build](https://gohugo.io/hugo-pipes/js) 的导入映射。此文件旨在帮助在诸如 [VS Code](https://code.visualstudio.com/) 等代码编辑器内进行智能感知/导航。请注意，如果您不使用 `js.Build`，则不会写入任何文件。

## Configure Server -> [server]

​	仅在运行 `hugo server` 时相关，在开发过程中可以设置 HTTP 标头，从而可以测试您的内容安全策略等。配置格式与 [Netlify](https://docs.netlify.com/routing/headers/#syntax-for-the-netlify-configuration-file) 的格式相匹配，并具有略微更强大的[全局匹配功能](https://github.com/gobwas/glob)：

config.

=== "yaml"

    ```yaml
    server:
      headers:
      - for: /**
        values:
          Content-Security-Policy: script-src localhost:1313
          Referrer-Policy: strict-origin-when-cross-origin
          X-Content-Type-Options: nosniff
          X-Frame-Options: DENY
          X-XSS-Protection: 1; mode=block
    ```

=== "toml"

    ```toml
    [server]
    [[server.headers]]
      for = '/**'
      [server.headers.values]
        Content-Security-Policy = 'script-src localhost:1313'
        Referrer-Policy = 'strict-origin-when-cross-origin'
        X-Content-Type-Options = 'nosniff'
        X-Frame-Options = 'DENY'
        X-XSS-Protection = '1; mode=block'
    ```

=== "json"

    ```json
    {
       "server": {
          "headers": [
             {
                "for": "/**",
                "values": {
                   "Content-Security-Policy": "script-src localhost:1313",
                   "Referrer-Policy": "strict-origin-when-cross-origin",
                   "X-Content-Type-Options": "nosniff",
                   "X-Frame-Options": "DENY",
                   "X-XSS-Protection": "1; mode=block"
                }
             }
          ]
       }
    }
    ```

​	由于这仅适用于"development only"，因此将其放置在`development`环境下可能是有意义的：

config/development/server.

=== "yaml"

    ```yaml
    headers:
    - for: /**
      values:
        Content-Security-Policy: script-src localhost:1313
        Referrer-Policy: strict-origin-when-cross-origin
        X-Content-Type-Options: nosniff
        X-Frame-Options: DENY
        X-XSS-Protection: 1; mode=block
    ```

=== "toml"

    ```toml
    [[headers]]
    for = '/**'
    [headers.values]
      Content-Security-Policy = 'script-src localhost:1313'
      Referrer-Policy = 'strict-origin-when-cross-origin'
      X-Content-Type-Options = 'nosniff'
      X-Frame-Options = 'DENY'
      X-XSS-Protection = '1; mode=block'
    ```

=== "json"

    ```json
    {
       "headers": [
          {
             "for": "/**",
             "values": {
                "Content-Security-Policy": "script-src localhost:1313",
                "Referrer-Policy": "strict-origin-when-cross-origin",
                "X-Content-Type-Options": "nosniff",
                "X-Frame-Options": "DENY",
                "X-XSS-Protection": "1; mode=block"
             }
          }
       ]
    }
    ```

​	您还可以为服务器指定简单的重定向规则。 语法与Netlify类似。

​	请注意，`status`200会触发[URL重写](https://docs.netlify.com/routing/redirects/rewrites-proxies/)，这是在SPA情况下所需要的，例如：

config/development/server.

=== "yaml"

    ```yaml
    redirects:
    - force: false
      from: /myspa/**
      status: 200
      to: /myspa/
    ```

=== "toml"

    ```toml
    [[redirects]]
    force = false
    from = '/myspa/**'
    status = 200
    to = '/myspa/'
    ```

=== "json"

    ```json
    {
       "redirects": [
          {
             "force": false,
             "from": "/myspa/**",
             "status": 200,
             "to": "/myspa/"
          }
       ]
    }
    ```

​	设置`force=true`将使重定向即使路径中存在现有内容也会生效。 请注意，在Hugo 0.76之前，`force`是默认行为，但这符合Netlify的处理方式。

## 404服务器错误页面 -> [[redirects]]

[New in v0.103.0](https://github.com/gohugoio/hugo/releases/tag/v0.103.0)

​	当运行`hugo server`时，默认情况下，Hugo将使用`404.html`模板呈现所有404错误。 请注意，如果您已经添加了一个或多个重定向到[服务器配置](https://gohugo.io/getting-started/configuration/#configure-server)中，则需要显式添加404重定向，例如：

config/development/server.

=== "yaml"

    ```yaml
    redirects:
    - from: /**
      status: 404
      to: /404.html
    ```

=== "toml"

    ```toml
    [[redirects]]
    from = '/**'
    status = 404
    to = '/404.html'
    ```

=== "json"

    ```json
    {
       "redirects": [
          {
             "from": "/**",
             "status": 404,
             "to": "/404.html"
          }
       ]
    }
    ```

## 配置标题大小写 -> titleCaseStyle

​	设置`titleCaseStyle`以指定[title](https://gohugo.io/functions/title/)模板函数和Hugo中自动部分标题使用的标题样式。

​	默认情况下，Hugo遵循[美联社 （Associated Press（AP））](https://www.apstylebook.com/)风格指南中的大写规则。 如果您想遵循[芝加哥风格（Chicago Manual of Style）](https://www.chicagomanualofstyle.org/home.html)手册，则将`titleCaseStyle`设置为`chicago`，或将其设置为`go`以使用Go的惯例，即每个单词都大写。

## 配置环境变量 

- HUGO_NUMWORKERMULTIPLIER

  可以设置为增加或减少在Hugo中并行处理中使用的工作程序数量。 如果未设置，则将使用逻辑CPU的数量。

## 配置查找顺序 

​	与模板[查找顺序](https://gohugo.io/templates/lookup-order/)类似，Hugo有一组默认规则，用于在站点源目录的根目录中搜索配置文件作为默认行为：

1. `./config.toml`
2. `./config.yaml`
3. `./config.json`

​	在`config`文件中，您可以指导Hugo如何渲染您的站点，控制您的站点菜单，并任意定义特定于您的项目的站点范围（site-wide）参数。

## 示例配置 

​	以下是典型的配置文件示例。在`params:`下嵌套的值将填充`.Site.Params`变量，供[模板](https://gohugo.io/templates/)使用：

config.

=== "yaml"

    ```yaml
    baseURL: https://yoursite.example.com/
    params:
      AuthorName: Jon Doe
      GitHubUser: spf13
      ListOfFoo:
      - foo1
      - foo2
      SidebarRecentLimit: 5
      Subtitle: Hugo is Absurdly Fast!
    permalinks:
      posts: /:year/:month/:title/
    title: My Hugo Site
    ```

=== "toml"

    ```toml
    baseURL = 'https://yoursite.example.com/'
    title = 'My Hugo Site'
    [params]
      AuthorName = 'Jon Doe'
      GitHubUser = 'spf13'
      ListOfFoo = ['foo1', 'foo2']
      SidebarRecentLimit = 5
      Subtitle = 'Hugo is Absurdly Fast!'
    [permalinks]
      posts = '/:year/:month/:title/'
    ```

=== "json"

    ```json
    {
       "baseURL": "https://yoursite.example.com/",
       "params": {
          "AuthorName": "Jon Doe",
          "GitHubUser": "spf13",
          "ListOfFoo": [
             "foo1",
             "foo2"
          ],
          "SidebarRecentLimit": 5,
          "Subtitle": "Hugo is Absurdly Fast!"
       },
       "permalinks": {
          "posts": "/:year/:month/:title/"
       },
       "title": "My Hugo Site"
    }
    ```

## 使用环境变量配置 

​	除了已经提到的三个配置选项外，可以通过操作系统环境变量定义配置键值。

​	例如，以下命令将在类Unix系统上有效地设置站点标题：

```txt
$ env HUGO_TITLE="Some Title" hugo
```

​	如果您使用像Netlify这样的服务部署您的站点，则这非常有用。请参阅Hugo文档中的[Netlify配置文件示例](https://github.com/gohugoio/hugoDocs/blob/master/netlify.toml)。

> ​	名称必须以`HUGO_`为前缀，并且设置操作系统环境变量时必须将配置键设置为大写。
>
> ​	要设置配置参数，请使用`HUGO_PARAMS_`作为前缀。
>

​	如果您使用了下划线命名法，则上述方法将无法正常工作。Hugo通过`HUGO`之后的第一个字符确定要使用的分隔符。这允许您使用任何[允许的](https://stackoverflow.com/questions/2821043/allowed-characters-in-linux-environment-variable-names#:~:text=So names may contain any,not begin with a digit)分隔符来定义形式为`HUGOxPARAMSxAPI_KEY=abcdefgh`的环境变量。

## 忽略内容和数据文件的渲染  -> ignoreFiles

​	注意：这个方法可行，但我们建议您使用更新且更强大的[includeFiles和excludeFiles](https://gohugo.io/hugo-modules/configuration/#module-config-mounts)挂载选项。

​	要在渲染站点时排除特定的`content`和`data`目录中的文件，请将`ignoreFiles`设置为一个或多个正则表达式，以匹配绝对文件路径。

​	要忽略以`.foo`或`.boo`结尾的文件：

=== "yaml"

    ```yaml
    ignoreFiles:
    - \.foo$
    - \.boo$
    ```

=== "toml"

    ```toml
    ignoreFiles = ['\.foo$', '\.boo$']
    ```

=== "json"

    ```json
    {
       "ignoreFiles": [
          "\\.foo$",
          "\\.boo$"
       ]
    }
    ```

​	通过绝对文件路径忽略一个文件：

=== "yaml"

    ```yaml
    ignoreFiles:
    - ^/home/user/project/content/test\.md$
    ```

=== "toml"

    ```toml
    ignoreFiles = ['^/home/user/project/content/test\.md$']
    ```

=== "json"

    ```json
    {
       "ignoreFiles": [
          "^/home/user/project/content/test\\.md$"
       ]
    }
    ```

## 配置Front Matter -> [frontmatter]

### 配置日期 

​	日期在Hugo中很重要，您可以通过向`config.toml`添加`frontmatter`部分来配置Hugo如何为您的内容页面分配日期。

默认配置如下：

config.

=== "yaml"

    ```yaml
    frontmatter:
      date:
      - date
      - publishDate
      - lastmod
      expiryDate:
      - expiryDate
      lastmod:
      - :git
      - lastmod
      - date
      - publishDate
      publishDate:
      - publishDate
      - date
    ```

=== "toml"

    ```toml
    [frontmatter]
      date = ['date', 'publishDate', 'lastmod']
      expiryDate = ['expiryDate']
      lastmod = [':git', 'lastmod', 'date', 'publishDate']
      publishDate = ['publishDate', 'date']
    ```

=== "json"

    ```json
    {
       "frontmatter": {
          "date": [
             "date",
             "publishDate",
             "lastmod"
          ],
          "expiryDate": [
             "expiryDate"
          ],
          "lastmod": [
             ":git",
             "lastmod",
             "date",
             "publishDate"
          ],
          "publishDate": [
             "publishDate",
             "date"
          ]
       }
    }
    ```

​	如果您的一些内容中具有非标准日期参数，您可以覆盖`date`的设置：

config.

=== "yaml"

    ```yaml
    frontmatter:
      date:
      - myDate
      - :default
    ```

=== "toml"

    ```toml
    [frontmatter]
      date = ['myDate', ':default']
    ```

=== "json"

    ```json
    {
       "frontmatter": {
          "date": [
             "myDate",
             ":default"
          ]
       }
    }
    ```

​	`:default`是默认设置的快捷方式。以上设置将根据需要将`.Date`设置为`myDate`中的日期值，如果不存在，则会查找`date`、`publishDate`、`lastmod`并选择第一个有效日期。

​	在右侧的列表中，以"`:`"开头的值是具有特殊含义的日期处理程序（见下文）。其他的只是您的正文数据配置中日期参数的名称（大小写不敏感）。另请注意，Hugo有一些内置别名：`lastmod` => `modified`，`publishDate` => `pubdate`，`published`和`expiryDate` => `unpublishdate`。例如，使用front matter中的`pubDate`作为日期将默认分配给`.PublishDate`。

​	特殊日期处理程序为：

- `:fileModTime`

  从内容文件的最后修改时间戳中提取日期。 

例如：

config.

=== "yaml"

    ```yaml
    frontmatter:
      lastmod:
      - lastmod
      - :fileModTime
      - :default
    ```

=== "toml"

    ```toml
    [frontmatter]
      lastmod = ['lastmod', ':fileModTime', ':default']
    ```

=== "json"

    ```json
    {
       "frontmatter": {
          "lastmod": [
             "lastmod",
             ":fileModTime",
             ":default"
          ]
       }
    }
    ```

​	上面的配置将首先尝试从front matter参数中`lastmod` 提取`.Lastmod`的值，然后再从内容文件的修改时间戳中提取日期值。最后，`:default`在这里不需要，但是Hugo最终会在`:git`、`date`和`publishDate`中查找有效的日期。

- `:filename`

  从内容文件的文件名中提取日期。例如，`2018-02-22-mypage.md`将提取日期`2018-02-22`。此外，如果`slug`未设置，则`mypage`将作为`.Slug`的值。 

例如：

config.

=== "yaml"

    ```yaml
    frontmatter:
      date:
      - :filename
      - :default
    ```

=== "toml"

    ```toml
    [frontmatter]
      date = [':filename', ':default']
    ```

=== "json"

    ```json
    {
       "frontmatter": {
          "date": [
             ":filename",
             ":default"
          ]
       }
    }
    ```

​	以上配置将首先尝试从文件名中提取`.Date`的值，然后再从front matter参数的`date`、`publishDate`和`lastmod`中查找。

- `:git`

  这是此内容文件的最后修订版的Git作者日期。这只有在设置了 `--enableGitInfo` 或在站点配置中设置了 `enableGitInfo = true` 时才会被设置。

## 配置其他输出格式 

​	Hugo v0.20引入了将内容呈现为多种输出格式（例如JSON、AMP html或CSV）的能力。请参阅[输出格式](https://gohugo.io/templates/output-formats/)，了解如何将这些值添加到您的Hugo项目配置文件中。

## 配置压缩 -> [minify]

默认配置：

config.

=== "yaml"

    ```yaml
    minify:
      disableCSS: false
      disableHTML: false
      disableJS: false
      disableJSON: false
      disableSVG: false
      disableXML: false
      minifyOutput: false
      tdewolff:
        css:
          keepCSS2: true
          precision: 0
        html:
          keepComments: false
          keepConditionalComments: true
          keepDefaultAttrVals: true
          keepDocumentTags: true
          keepEndTags: true
          keepQuotes: false
          keepWhitespace: false
        js:
          keepVarNames: false
          noNullishOperator: false
          precision: 0
        json:
          keepNumbers: false
          precision: 0
        svg:
          keepComments: false
          precision: 0
        xml:
          keepWhitespace: false
    ```

=== "toml"

    ```toml
    [minify]
      disableCSS = false
      disableHTML = false
      disableJS = false
      disableJSON = false
      disableSVG = false
      disableXML = false
      minifyOutput = false
      [minify.tdewolff]
        [minify.tdewolff.css]
          keepCSS2 = true
          precision = 0
        [minify.tdewolff.html]
          keepComments = false
          keepConditionalComments = true
          keepDefaultAttrVals = true
          keepDocumentTags = true
          keepEndTags = true
          keepQuotes = false
          keepWhitespace = false
        [minify.tdewolff.js]
          keepVarNames = false
          noNullishOperator = false
          precision = 0
        [minify.tdewolff.json]
          keepNumbers = false
          precision = 0
        [minify.tdewolff.svg]
          keepComments = false
          precision = 0
        [minify.tdewolff.xml]
          keepWhitespace = false
    ```

=== "json"

    ```json
    {
       "minify": {
          "disableCSS": false,
          "disableHTML": false,
          "disableJS": false,
          "disableJSON": false,
          "disableSVG": false,
          "disableXML": false,
          "minifyOutput": false,
          "tdewolff": {
             "css": {
                "keepCSS2": true,
                "precision": 0
             },
             "html": {
                "keepComments": false,
                "keepConditionalComments": true,
                "keepDefaultAttrVals": true,
                "keepDocumentTags": true,
                "keepEndTags": true,
                "keepQuotes": false,
                "keepWhitespace": false
             },
             "js": {
                "keepVarNames": false,
                "noNullishOperator": false,
                "precision": 0
             },
             "json": {
                "keepNumbers": false,
                "precision": 0
             },
             "svg": {
                "keepComments": false,
                "precision": 0
             },
             "xml": {
                "keepWhitespace": false
             }
          }
       }
    }
    ```



## 配置文件缓存 -> [caches]

​	自Hugo 0.52版本以来，您可以配置的不仅是`cacheDir`。这是默认配置：

=== "yaml"

    ```yaml
    caches:
      assets:
        dir: :resourceDir/_gen
        maxAge: -1
      getcsv:
        dir: :cacheDir/:project
        maxAge: -1
      getjson:
        dir: :cacheDir/:project
        maxAge: -1
      getresource:
        dir: :cacheDir/:project
        maxAge: -1
      images:
        dir: :resourceDir/_gen
        maxAge: -1
      modules:
        dir: :cacheDir/modules
        maxAge: -1
    ```

=== "toml"

    ```toml
    [caches]
      [caches.assets]
        dir = ':resourceDir/_gen'
        maxAge = -1
      [caches.getcsv]
        dir = ':cacheDir/:project'
        maxAge = -1
      [caches.getjson]
        dir = ':cacheDir/:project'
        maxAge = -1
      [caches.getresource]
        dir = ':cacheDir/:project'
        maxAge = -1
      [caches.images]
        dir = ':resourceDir/_gen'
        maxAge = -1
      [caches.modules]
        dir = ':cacheDir/modules'
        maxAge = -1
    ```

=== "json"

    ```json
    {
       "caches": {
          "assets": {
             "dir": ":resourceDir/_gen",
             "maxAge": -1
          },
          "getcsv": {
             "dir": ":cacheDir/:project",
             "maxAge": -1
          },
          "getjson": {
             "dir": ":cacheDir/:project",
             "maxAge": -1
          },
          "getresource": {
             "dir": ":cacheDir/:project",
             "maxAge": -1
          },
          "images": {
             "dir": ":resourceDir/_gen",
             "maxAge": -1
          },
          "modules": {
             "dir": ":cacheDir/modules",
             "maxAge": -1
          }
       }
    }
    ```

​	您可以在自己的`config.toml`中覆盖这些缓存设置。

### 关键字的解释 

- `:cacheDir`

  这是`cacheDir`配置选项的值，如果设置了的话（也可以通过OS环境变量`HUGO_CACHEDIR`设置）。如果在Netlify上，将回退到`/opt/build/cache/hugo_cache/`，对于其他的操作系统，将位于操作系统临时目录下的`hugo_cache`目录。这意味着，如果您在Netlify上运行构建，所有配置为`:cacheDir`的缓存都将保存并在下一次构建时恢复。对于其他的CI供应商，请阅读其文档。有关CircleCI示例，请参见[此配置](https://github.com/bep/hugo-sass-test/blob/6c3960a8f4b90e8938228688bc49bdcdd6b2d99e/.circleci/config.yml)。 

- `:project`

  当前Hugo项目的基本目录名称。这意味着，在默认设置中，每个项目都有单独的文件缓存，这意味着当您运行`hugo --gc`时，您不会触及与其他在同一台电脑上运行的Hugo项目相关的文件。 

- `:resourceDir`

  这是`resourceDir`配置选项的值。 

- maxAge

  这是缓存条目被清除之前的持续时间，-1表示永远，0有效地关闭该特定缓存。使用Go的`time.Duration`，所以有效值是`"10s"`（10秒），`"10m"`（10分钟）和`"10h"`（10小时）。 

- dir

  这是用于存储此缓存文件的绝对路径。允许的起始占位符是`:cacheDir`和`:resourceDir`（见上文）。 

## 配置格式规范 

- [TOML 规范](https://github.com/toml-lang/toml)
- [YAML 规范](https://yaml.org/spec/)
- [JSON 规范](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)

## 参见 

- [数据模板 ](https://gohugo.io/templates/data-templates/)
- [前置元数据](https://gohugo.io/content-management/front-matter/)
- [配置标记](https://gohugo.io/getting-started/configuration-markup/)
- [在GitLab上托管](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)
- [Hugo和一般数据保护条例（GDPR）](https://gohugo.io/about/hugo-and-gdpr/)
