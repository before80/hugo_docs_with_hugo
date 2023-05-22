+++
title = "多语言模式"
weight = 22
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Multilingual Mode - 多语言模式 

[https://gohugo.io/content-management/multilingual/](https://gohugo.io/content-management/multilingual/)

​	Hugo支持创建并排展示多种语言的站点。

​	您应该在站点配置中的`languages`部分定义可用的语言。

​	另请参阅[Hugo多语言第一部分：内容翻译](https://regisphilibert.com/blog/2018/08/hugo-multilingual-part-1-managing-content-translation/)。

## 配置语言 

​	以下是多语言Hugo项目的站点配置示例：

config.

=== "yaml"

    ``` yaml
    copyright: Everything is mine
    defaultContentLanguage: en
    languages:
      ar:
        languagedirection: rtl
        title: مدونتي
        weight: 2
      en:
        params:
          linkedin: https://linkedin.com/whoever
        title: My blog
        weight: 1
      fr:
        params:
          linkedin: https://linkedin.com/fr/whoever
          navigation:
            help: Aide
        title: Mon blogue
        weight: 2
      pt-pt:
        title: O meu blog
        weight: 3
    params:
      navigation:
        help: Help
    ```

=== "toml"

    ``` toml
    copyright = 'Everything is mine'
    defaultContentLanguage = 'en'
    [languages]
      [languages.ar]
        languagedirection = 'rtl'
        title = 'مدونتي'
        weight = 2
      [languages.en]
        title = 'My blog'
        weight = 1
        [languages.en.params]
          linkedin = 'https://linkedin.com/whoever'
      [languages.fr]
        title = 'Mon blogue'
        weight = 2
        [languages.fr.params]
          linkedin = 'https://linkedin.com/fr/whoever'
          [languages.fr.params.navigation]
            help = 'Aide'
      [languages.pt-pt]
        title = 'O meu blog'
        weight = 3
    [params]
      [params.navigation]
        help = 'Help'
    ```

=== "json"

    ``` json
    {
       "copyright": "Everything is mine",
       "defaultContentLanguage": "en",
       "languages": {
          "ar": {
             "languagedirection": "rtl",
             "title": "مدونتي",
             "weight": 2
          },
          "en": {
             "params": {
                "linkedin": "https://linkedin.com/whoever"
             },
             "title": "My blog",
             "weight": 1
          },
          "fr": {
             "params": {
                "linkedin": "https://linkedin.com/fr/whoever",
                "navigation": {
                   "help": "Aide"
                }
             },
             "title": "Mon blogue",
             "weight": 2
          },
          "pt-pt": {
             "title": "O meu blog",
             "weight": 3
          }
       },
       "params": {
          "navigation": {
             "help": "Help"
          }
       }
    }
    ```



​	任何未在`languages`块中定义的内容都将回退到该键的全局值（例如英语`en`语言的`copyright`）。这也适用于`params`，如上面的示例所示：您将在法语中获得`Aide`的值，并在所有没有设置此参数的语言中获得`Help`。

​	使用上述配置，所有内容、站点地图、RSS源、分页和分类页将在英语（默认内容语言）下的`/`目录下渲染，然后在法语的`/fr`目录下渲染。

​	在[单页模板](https://gohugo.io/templates/single-page-templates/)中使用前置元数据 `Params`时，忽略翻译的键中的`params`。

​	`defaultContentLanguage`设置项目的默认语言。如果未设置，则默认语言为`en`。

​	如果需要将默认语言渲染在其自己的语言代码（`/en`）下，像其他语言一样，请设置`defaultContentLanguageInSubdir：true`。

​	只有明显的非全局选项可以按语言覆盖。全局选项的示例包括`baseURL`、`buildDrafts`等。

请注意：使用小写语言代码，即使是使用区域性语言（例如使用pt-pt而不是pt-PT）。当前Hugo语言内部将语言代码转换为小写字母，这可能会与未转换为小写字母的`defaultContentLanguage`等设置发生冲突。请在[Hugo存储库问题跟踪器](https://github.com/gohugoio/hugo/issues/7344)中跟踪此问题的演变。

### 禁用语言 

​	您可以禁用一个或多个语言。这在进行新翻译时非常有用。

config.

=== "yaml"

    ``` yaml
    disableLanguages:
    - fr
    - ja
    ```

=== "toml"

    ``` toml
    disableLanguages = ['fr', 'ja']
    ```

=== "json"

    ``` json
    {
       "disableLanguages": [
          "fr",
          "ja"
       ]
    }
    ```



​	请注意，您不能禁用默认内容语言。

​	我们将其保留为一个独立的设置，以便更容易通过[操作系统环境](https://gohugo.io/getting-started/configuration/#configure-with-environment-variables)进行设置：

```bash
HUGO_DISABLELANGUAGES="fr ja" hugo
```

​	如果您已经在`config.toml`中有禁用的语言列表，可以像这样在开发环境中启用它们：

```bash
HUGO_DISABLELANGUAGES=" " hugo server
```

### 配置多语言Multihost 

​	从Hugo 0.31开始，我们支持多语言multihost配置。详见[此问题](https://github.com/gohugoio/hugo/issues/4027)的说明。

​	这意味着现在可以为每种`language`配置一个`baseURL`：

> 如果在`language`级别上设置了 `baseURL`，则所有语言都必须具有一个，且它们必须全部不同。

例如：

config.

=== "yaml"

    ``` yaml
    languages:
      en:
        baseURL: https://example.com
        languageName: English
        title: In English
        weight: 2
      fr:
        baseURL: https://example.fr
        languageName: Français
        title: En Français
        weight: 1
    ```

=== "toml"

    ``` toml
    [languages]
      [languages.en]
        baseURL = 'https://example.com'
        languageName = 'English'
        title = 'In English'
        weight = 2
      [languages.fr]
        baseURL = 'https://example.fr'
        languageName = 'Français'
        title = 'En Français'
        weight = 1
    ```

=== "json"

    ``` json
    {
       "languages": {
          "en": {
             "baseURL": "https://example.com",
             "languageName": "English",
             "title": "In English",
             "weight": 2
          },
          "fr": {
             "baseURL": "https://example.fr",
             "languageName": "Français",
             "title": "En Français",
             "weight": 1
          }
       }
    }
    ```

​	有了上面的配置，这两个站点将生成到带有自己根目录的 `public` 中：

```text
public
├── en
└── fr
```

​	所有的URL（例如`.Permalink`等）都将从该根目录生成。因此，上面的英文主页的`.Permalink`将设置为https://example.com/。

​	当您运行`hugo server`时，我们将启动多个HTTP服务器。您通常会在控制台中看到以下内容：

```text
Web Server is available at 127.0.0.1:1313 (bind address 127.0.0.1)
Web Server is available at 127.0.0.1:1314 (bind address 127.0.0.1)
Press Ctrl+C to stop
```

​	实时重新加载和在服务器之间使用`--navigateToChanged`会按预期工作。

## 翻译您的内容 

​	有两种管理内容翻译的方式。两种方式都可以确保每个页面都被分配了一种语言，并与其对应的翻译链接在一起。

### 按文件名翻译 

​	考虑以下示例：

1. `/content/about.en.md`
2. `/content/about.fr.md`

​	第一个文件分配了英语语言，并链接到第二个文件。第二个文件分配了法语语言，并链接到第一个文件。

​	它们的语言是根据文件名后缀添加的语言代码分配的。

​	通过具有相同的路径和基本文件名，将内容部分链接在一起作为翻译页面。

​	如果文件没有语言代码，它将被分配为默认语言。

### 按内容目录翻译 

​	该系统使用不同的内容目录来处理每种语言。每种语言的内容目录都是使用 `contentDir` 参数设置的。

config.

=== "yaml"

    ``` yaml
    languages:
      en:
        contentDir: content/english
        languageName: English
        weight: 10
      fr:
        contentDir: content/french
        languageName: Français
        weight: 20
    ```

=== "toml"

    ``` toml
    [languages]
      [languages.en]
        contentDir = 'content/english'
        languageName = 'English'
        weight = 10
      [languages.fr]
        contentDir = 'content/french'
        languageName = 'Français'
        weight = 20
    ```

=== "json"

    ``` json
    {
       "languages": {
          "en": {
             "contentDir": "content/english",
             "languageName": "English",
             "weight": 10
          },
          "fr": {
             "contentDir": "content/french",
             "languageName": "Français",
             "weight": 20
          }
       }
    }
    ```



​	`contentDir` 的值可以是任何有效的路径，甚至是绝对路径引用。唯一的限制是内容目录不能重叠。

​	考虑以下示例与上述配置一起使用：

1. `/content/english/about.md`
2. `/content/french/about.md`

​	第一个文件被分配为英语，并与第二个文件链接。第二个文件被分配为法语，并与第一个文件链接。

​	它们的语言是根据它们放置所在的内容目录分配的。

​	通过具有相同的路径和基名（相对于其语言内容目录），内容片段将作为翻译页面相互链接。

### 绕过默认链接 

​	任何在前置元数据中设置相同翻译键（`translationKey`）的页面将被链接为翻译页面，而不考虑基名或位置。

​	考虑以下示例：

1. `/content/about-us.en.md`
2. `/content/om.nn.md`
3. `/content/presentation/a-propos.fr.md`

=== "yaml"

    ``` yaml
    translationKey: about
    ```

=== "toml"

    ``` toml
    translationKey = 'about'
    ```

=== "json"

    ``` json
    {
       "translationKey": "about"
    }
    ```

​	通过在所有三个页面的前置元数据参数中设置翻译键（`translationKey`）为 `about`，它们将被链接为翻译页面。

### 本地化永久链接 

​	因为路径和文件名用于处理链接，所有翻译页面将共享相同的URL（除了语言子目录）。

​	为了本地化URL：

- 对于常规页面，在前置元数据中设置`slug`或`url` 
- 对于章节页面，在前置元数据中设置`url` 

​	例如，法语翻译可以有自己本地化的`slug`。

content/about.fr.md

=== "yaml"

    ``` yaml
    ---
    slug: a-propos
    title: A Propos
    ---
    ```

=== "toml"

    ``` toml
    +++
    slug = 'a-propos'
    title = 'A Propos'
    +++
    ```

=== "json"

    ``` json
    {
       "slug": "a-propos",
       "title": "A Propos"
    }
    ```

At render, Hugo will build both `/about/` and `/fr/a-propos/` without affecting the translation link.

​	在渲染时，Hugo将同时构建`/about/`和`/fr/a-propos/`，而不影响翻译链接。

### 页面 Bundles 

To avoid the burden of having to duplicate files, each Page Bundle inherits the resources of its linked translated pages’ bundles except for the content files (Markdown files, HTML files etc…).

为了避免重复文件的负担，每个页面包继承其链接的翻译页面包的资源，除了内容文件（Markdown文件，HTML文件等）。

Therefore, from within a template, the page will have access to the files from all linked pages’ bundles.

因此，在模板内，页面将可以访问所有链接页面包的文件。

If, across the linked bundles, two or more files share the same basename, only one will be included and chosen as follows:

如果在链接的包中，两个或多个文件具有相同的基名，则只包括一个，并按以下方式选择：

- File from current language bundle, if present.
- 当前语言包中的文件（如果存在）。 
- First file found across bundles by order of language `Weight`.
- 按语言权重顺序在所有包中找到的第一个文件。 

Page Bundle resources follow the same language assignment logic as content files, both by filename (`image.jpg`, `image.fr.jpg`) and by directory (`english/about/header.jpg`, `french/about/header.jpg`).

页面包资源遵循与内容文件相同的语言分配逻辑，包括文件名（image.jpg，image.fr.jpg）和目录（english/about/header.jpg，french/about/header.jpg）。

## 引用翻译内容 

To create a list of links to translated content, use a template similar to the following:

要创建链接到翻译内容的链接列表，请使用类似以下的模板：

layouts/partials/i18nlist.html



```go-html-template
{{ if .IsTranslated }}
<h4>{{ i18n "translations" }}</h4>
<ul>
  {{ range .Translations }}
  <li>
    <a href="{{ .Permalink }}">{{ .Lang }}: {{ .Title }}{{ if .IsPage }} ({{ i18n "wordCount" . }}){{ end }}</a>
  </li>
  {{ end }}
</ul>
{{ end }}
```

The above can be put in a `partial` (i.e., inside `layouts/partials/`) and included in any template, whether a [single content page](https://gohugo.io/templates/single-page-templates/) or the [homepage](https://gohugo.io/templates/homepage/). It will not print anything if there are no translations for a given page.

上述内容可以放在partial中（即layouts/partials/文件夹中），并包含在任何模板中，无论是单个内容页面还是主页。如果没有给定页面的翻译，它将不会打印任何内容。

The above also uses the [`i18n` function](https://gohugo.io/functions/i18n/) described in the next section.

上述内容还使用了下一节中描述的i18n函数。

### 列出所有可用语言 

`.AllTranslations` on a `Page` can be used to list all translations, including the page itself. On the home page it can be used to build a language navigator:

在页面上使用.AllTranslations可以列出所有翻译，包括页面本身。在主页上，它可用于构建语言导航器：

layouts/partials/allLanguages.html

```go-html-template
<ul>
{{ range $.Site.Home.AllTranslations }}
<li><a href="{{ .Permalink }}">{{ .Language.LanguageName }}</a></li>
{{ end }}
</ul>
```

## 字符串翻译 

Hugo uses [go-i18n](https://github.com/nicksnyder/go-i18n) to support string translations. [See the project’s source repository](https://github.com/nicksnyder/go-i18n) to find tools that will help you manage your translation workflows.

Hugo使用go-i18n支持字符串翻译。请参见该项目的源存储库，以查找可帮助您管理翻译工作流程的工具。

Translations are collected from the `themes/<THEME>/i18n/` folder (built into the theme), as well as translations present in `i18n/` at the root of your project. In the `i18n`, the translations will be merged and take precedence over what is in the theme folder. Language files should be named according to [RFC 5646](https://tools.ietf.org/html/rfc5646) with names such as `en-US.toml`, `fr.toml`, etc.

从themes/<THEME>/i18n/文件夹（内置于主题中）以及位于项目根目录的i18n/文件夹中收集翻译。在i18n中，翻译将合并并优先于主题文件夹中的内容。语言文件应根据RFC 5646命名，例如en-US.toml、fr.toml等。

Artificial languages with private use subtags as defined in [RFC 5646 § 2.2.7](https://datatracker.ietf.org/doc/html/rfc5646#section-2.2.7) are also supported. You may omit the `art-x-` prefix for brevity. For example:

RFC 5646§2.2.7中定义的带有私有使用子标记的人工语言也受支持。为简洁起见，您可以省略art-x-前缀。例如：

```text
art-x-hugolang
hugolang
```

Private use subtags must not exceed 8 alphanumeric characters.

私有使用子标记不得超过8个字母数字字符。

### 查询基本翻译 

From within your templates, use the `i18n` function like this:

在您的模板中，可以像这样使用`i18n`函数：

```go-html-template
{{ i18n "home" }}
```

The function will search for the `"home"` id:

该函数将搜索"home"id：

i18n/en-US.

=== "yaml"

    ``` yaml
    home:
      other: Home
    ```

=== "toml"

    ``` toml
    [home]
      other = 'Home'
    ```

=== "json"

    ``` json
    {
       "home": {
          "other": "Home"
       }
    }
    ```

The result will be

结果将是

```text
Home
```

### 查询带有变量的灵活翻译 

Often you will want to use the page variables in the translation strings. To do so, pass the `.` context when calling `i18n`:

通常，您会想在翻译字符串中使用页面变量。要这样做，请在调用i18n时传递上下文。

```go-html-template
{{ i18n "wordCount" . }}
```

The function will pass the `.` context to the `"wordCount"` id:

该函数将把上下文传递给"wordCount"id：

i18n/en-US.

=== "yaml"

    ``` yaml
    wordCount:
      other: This article has {{ .WordCount }} words.
    ```

=== "toml"

    ``` toml
    [wordCount]
      other = 'This article has {{ .WordCount }} words.'
    ```

=== "json"

    ``` json
    {
       "wordCount": {
          "other": "This article has {{ .WordCount }} words."
       }
    }
    ```

Assume `.WordCount` in the context has value is 101. The result will be:

假设上下文中的 .WordCount 值为 101。结果将是：

```text
This article has 101 words.
```

### 查询单数/复数翻译 

In other to meet singular/plural requirement, you must pass a dictionary (map) with a numeric `.Count` property to the `i18n` function. The below example uses `.ReadingTime` variable which has a built-in `.Count` property.

为了满足单数/复数要求，您必须将具有数字 .Count 属性的字典（map）传递给 i18n 函数。下面的示例使用内置的 .ReadingTime 变量，它具有一个 .Count 属性。

```go-html-template
{{ i18n "readingTime" .ReadingTime }}
```

The function will read `.Count` from `.ReadingTime` and evaluate whether the number is singular (`one`) or plural (`other`). After that, it will pass to `readingTime` id in `i18n/en-US.toml` file:

函数将从 .ReadingTime 中读取 .Count 并评估数字是单数（one）还是复数（other）。之后，它将传递给 i18n/en-US.toml 文件中的 readingTime id：

i18n/en-US.

=== "yaml"

    ``` yaml
    readingTime:
      one: One minute to read
      other: '{{ .Count }} minutes to read'
    ```

=== "toml"

    ``` toml
    [readingTime]
      one = 'One minute to read'
      other = '{{ .Count }} minutes to read'
    ```

=== "json"

    ``` json
    {
       "readingTime": {
          "one": "One minute to read",
          "other": "{{ .Count }} minutes to read"
       }
    }
    ```



Assuming `.ReadingTime.Count` in the context has value is 525600. The result will be:

假设上下文中的 .ReadingTime.Count 值为 525600。结果将是：

```text
525600 minutes to read
```

If `.ReadingTime.Count` in the context has value is 1. The result is:

如果上下文中的 .ReadingTime.Count 值为1。结果是：

```text
One minute to read
```

In case you need to pass a custom data: (`(dict "Count" numeric_value_only)` is minimum requirement)

如果您需要传递自定义数据：((dict "Count" numeric_value_only) 是最小要求)

```go-html-template
{{ i18n "readingTime" (dict "Count" 25 "FirstArgument" true "SecondArgument" false "Etc" "so on, so far") }}
```

## 本地化 

The following localization examples assume your site’s primary language is English, with translations to French and German.

以下本地化示例假定您站点的主要语言为英语，并提供了法语和德语的翻译。

config.

=== "yaml"

    ``` yaml
    defaultContentLanguage: en
    languages:
      de:
        contentDir: content/de
        languageName: Deutsch
        weight: 3
      en:
        contentDir: content/en
        languageName: English
        weight: 1
      fr:
        contentDir: content/fr
        languageName: Français
        weight: 2
    ```

=== "toml"

    ``` toml
    defaultContentLanguage = 'en'
    [languages]
      [languages.de]
        contentDir = 'content/de'
        languageName = 'Deutsch'
        weight = 3
      [languages.en]
        contentDir = 'content/en'
        languageName = 'English'
        weight = 1
      [languages.fr]
        contentDir = 'content/fr'
        languageName = 'Français'
        weight = 2
    ```

=== "json"

    ``` json
    {
       "defaultContentLanguage": "en",
       "languages": {
          "de": {
             "contentDir": "content/de",
             "languageName": "Deutsch",
             "weight": 3
          },
          "en": {
             "contentDir": "content/en",
             "languageName": "English",
             "weight": 1
          },
          "fr": {
             "contentDir": "content/fr",
             "languageName": "Français",
             "weight": 2
          }
       }
    }
    ```



### 日期 

With this 前置元数据:

有了这个前置元数据：

=== "yaml"

    ``` yaml
    date: 2021-11-03T12:34:56+01:00
    ```

=== "toml"

    ``` toml
    date = 2021-11-03T12:34:56+01:00
    ```

=== "json"

    ``` json
    {
       "date": "2021-11-03T12:34:56+01:00"
    }
    ```

And this template code:

以及这个模板代码：

```go-html-template
{{ .Date | time.Format ":date_full" }}
```

The rendered page displays:

渲染的页面显示：

| Language | Value                       |
| :------- | :-------------------------- |
| English  | Wednesday, November 3, 2021 |
| Français | mercredi 3 novembre 2021    |
| Deutsch  | Mittwoch, 3. November 2021  |

See [time.Format](https://gohugo.io/functions/dateformat) for details.

​	详细信息请参见[time.Format](https://gohugo.io/functions/dateformat)。

### 货币 Currency 

With this template code:

使用此模板代码：

```go-html-template
{{ 512.5032 | lang.FormatCurrency 2 "USD" }}
```

The rendered page displays:

渲染的页面显示：

| Language | Value      |
| :------- | :--------- |
| English  | $512.50    |
| Français | 512,50 $US |
| Deutsch  | 512,50 $   |

See [lang.FormatCurrency](https://gohugo.io/functions/lang) and [lang.FormatAccounting](https://gohugo.io/functions/lang) for details.

### 数字

With this template code:

使用此模板代码：

```go-html-template
{{ 512.5032 | lang.FormatNumber 2 }}
```

The rendered page displays:

渲染的页面显示：

| Language | Value  |
| :------- | :----- |
| English  | 512.50 |
| Français | 512,50 |
| Deutsch  | 512,50 |

See [lang.FormatNumber](https://gohugo.io/functions/lang) and [lang.FormatNumberCustom](https://gohugo.io/functions/lang) for details.

请参考lang.FormatNumber和lang.FormatNumberCustom了解详情。

### 百分数 

With this template code:

使用此模板代码：

```go-html-template
{{ 512.5032 | lang.FormatPercent 2 }} ---> 512.50%
```

The rendered page displays:

渲染的页面显示：

| Language | Value    |
| :------- | :------- |
| English  | 512.50%  |
| Français | 512,50 % |
| Deutsch  | 512,50 % |

See [lang.FormatPercent](https://gohugo.io/functions/lang) for details.

请参考lang.FormatPercent了解详情。

## 菜单 

Localization of menu entries depends on the how you define them:

菜单项的本地化取决于定义它们的方式：

- When you define menu entries [automatically](https://gohugo.io/content-management/menus/#define-automatically) using the section pages menu, you must use translation tables to localize each entry.
- 当您使用部分页面菜单自动定义菜单项时，您必须使用翻译表来本地化每个菜单项。 
- When you define menu entries [in 前置元数据](https://gohugo.io/content-management/menus/#define-in-front-matter), they are already localized based on the 前置元数据 itself. If the 前置元数据 values are insufficient, use translation tables to localize each entry.
- 当您在前置matter中定义菜单项时，它们已经基于前置matter本身进行了本地化。如果前置matter值不足，请使用翻译表来本地化每个菜单项。 
- When you define menu entries [in site configuration](https://gohugo.io/content-management/menus/#define-in-site-configuration), you can (a) use translation tables, or (b) create language-specific menu entries under each language key.
- 当您在站点配置中定义菜单项时，您可以（a）使用翻译表，或（b）在每个语言键下创建特定于语言的菜单项。 

### 使用翻译表 

When rendering the text that appears in menu each entry, the [example menu template](https://gohugo.io/templates/menu-templates/#example) does this:

在渲染出现在菜单中的文本时，示例菜单模板执行以下操作：

```go-html-template
{{ or (T .Identifier) .Name | safeHTML }}
```

It queries the translation table for the current language using the menu entry’s `identifier` and returns the translated string. If the translation table does not exist, or if the `identifier` key is not present in the translation table, it falls back to `name`.

它使用菜单项的标识符查询当前语言的翻译表，并返回已翻译的字符串。如果翻译表不存在，或者标识符键不在翻译表中，则回退到名称。

The `identifier` depends on how you define menu entries:

标识符取决于您如何定义菜单项：

- If you define the menu entry [automatically](https://gohugo.io/content-management/menus/#define-automatically) using the section pages menu, the `identifier` is the page’s `.Section`.
- 如果您使用部分页面菜单自动定义菜单项，则标识符是页面的.Section。 
- If you define the menu entry [in site configuration](https://gohugo.io/content-management/menus/#define-in-site-configuration) or [in 前置元数据](https://gohugo.io/content-management/menus/#define-in-front-matter), set the `identifier` property to the desired value.
- 如果您在站点配置或前置matter中定义菜单项，请将标识符属性设置为所需值。 

For example, if you define menu entries in site configuration:

例如，如果您在站点配置中定义菜单项：

config.

=== "yaml"

    ``` yaml
    menu:
      main:
      - identifier: products
        name: Products
        pageRef: /products
        weight: 10
      - identifier: services
        name: Services
        pageRef: /services
        weight: 20
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.main]]
      identifier = 'products'
      name = 'Products'
      pageRef = '/products'
      weight = 10
    [[menu.main]]
      identifier = 'services'
      name = 'Services'
      pageRef = '/services'
      weight = 20
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": [
             {
                "identifier": "products",
                "name": "Products",
                "pageRef": "/products",
                "weight": 10
             },
             {
                "identifier": "services",
                "name": "Services",
                "pageRef": "/services",
                "weight": 20
             }
          ]
       }
    }
    ```

Create corresponding entries in the translation tables:

创建相应的翻译表条目：

i18n/de.

=== "yaml"

    ``` yaml
    products: Produkte
    services: Leistungen
    ```

=== "toml"

    ``` toml
    products = 'Produkte'
    services = 'Leistungen'
    ```

=== "json"

    ``` json
    {
       "products": "Produkte",
       "services": "Leistungen"
    }
    ```



### 创建语言特定的菜单条目 

例如：

config.

=== "yaml"

    ``` yaml
    languages:
      de:
        languageCode: de-DE
        languageName: Deutsch
        menu:
          main:
          - name: Produkte
            pageRef: /products
            weight: 10
          - name: Leistungen
            pageRef: /services
            weight: 20
        weight: 1
      en:
        languageCode: en-US
        languageName: English
        menu:
          main:
          - name: Products
            pageRef: /products
            weight: 10
          - name: Services
            pageRef: /services
            weight: 20
        weight: 2
    ```

=== "toml"

    ``` toml
    [languages]
      [languages.de]
        languageCode = 'de-DE'
        languageName = 'Deutsch'
        weight = 1
        [languages.de.menu]
    [[languages.de.menu.main]]
          name = 'Produkte'
          pageRef = '/products'
          weight = 10
    [[languages.de.menu.main]]
          name = 'Leistungen'
          pageRef = '/services'
          weight = 20
      [languages.en]
        languageCode = 'en-US'
        languageName = 'English'
        weight = 2
        [languages.en.menu]
    [[languages.en.menu.main]]
          name = 'Products'
          pageRef = '/products'
          weight = 10
    [[languages.en.menu.main]]
          name = 'Services'
          pageRef = '/services'
          weight = 20
    ```

=== "json"

    ``` json
    {
       "languages": {
          "de": {
             "languageCode": "de-DE",
             "languageName": "Deutsch",
             "menu": {
                "main": [
                   {
                      "name": "Produkte",
                      "pageRef": "/products",
                      "weight": 10
                   },
                   {
                      "name": "Leistungen",
                      "pageRef": "/services",
                      "weight": 20
                   }
                ]
             },
             "weight": 1
          },
          "en": {
             "languageCode": "en-US",
             "languageName": "English",
             "menu": {
                "main": [
                   {
                      "name": "Products",
                      "pageRef": "/products",
                      "weight": 10
                   },
                   {
                      "name": "Services",
                      "pageRef": "/services",
                      "weight": 20
                   }
                ]
             },
             "weight": 2
          }
       }
    }
    ```



For a simple menu with two languages, these menu entries are easy to create and maintain. For a larger menu, or with more than two languages, using translation tables as described above is preferable.

对于只包含两种语言的简单菜单，这些菜单条目易于创建和维护。对于更大的菜单或包含两种以上语言的菜单，最好使用上述描述的翻译表。

## 缺少翻译 

If a string does not have a translation for the current language, Hugo will use the value from the default language. If no default value is set, an empty string will be shown.

如果一个字符串在当前语言下没有翻译，Hugo 将使用默认语言的值。如果没有设置默认值，则显示为空字符串。

While translating a Hugo website, it can be handy to have a visual indicator of missing translations. The [`enableMissingTranslationPlaceholders` configuration option](https://gohugo.io/getting-started/configuration/) will flag all untranslated strings with the placeholder `[i18n] identifier`, where `identifier` is the id of the missing translation.

在翻译 Hugo 站点时，有一个缺少翻译的可视化指示器会很方便。启用 enableMissingTranslationPlaceholders 配置选项会使用 [i18n] 占位符标记所有未翻译的字符串，其中 identifier 是缺失翻译的 id。

Hugo will generate your website with these missing translation placeholders. It might not be suitable for production environments.

Hugo 将生成带有这些缺失翻译占位符的站点。这可能不适合生产环境。

For merging of content from other languages (i.e. missing content translations), see [lang.Merge](https://gohugo.io/functions/lang.merge/).

要合并其他语言的内容（即缺失的内容翻译），请参阅 lang.Merge。

To track down missing translation strings, run Hugo with the `--printI18nWarnings` flag:

要追踪缺失的翻译字符串，请使用 --printI18nWarnings 标志运行 Hugo：

```bash
hugo --printI18nWarnings | grep i18n
i18n|MISSING_TRANSLATION|en|wordCount
```

## 多语言主题支持 

To support Multilingual mode in your themes, some considerations must be taken for the URLs in the templates. If there is more than one language, URLs must meet the following criteria:

要在主题中支持多语言模式，必须在模板中考虑 URL。如果有多种语言，则 URL 必须符合以下标准：

- Come from the built-in `.Permalink` or `.RelPermalink`
- 来自内置的 .Permalink 或 .RelPermalink 
- Be constructed with the [`relLangURL` template function](https://gohugo.io/functions/rellangurl) or the [`absLangURL` template function](https://gohugo.io/functions/abslangurl) **OR** be prefixed with `{{ .LanguagePrefix }}`
- 使用 relLangURL 模板函数或 absLangURL 模板函数构造 URL，或在 URL 前加上 {{.LanguagePrefix}} 

If there is more than one language defined, the `LanguagePrefix` variable will equal `/en` (or whatever your `CurrentLanguage` is). If not enabled, it will be an empty string (and is therefore harmless for single-language Hugo websites).

如果定义了多种语言，则 LanguagePrefix 变量将等于 /en（或您的 CurrentLanguage），如果未启用，则为空字符串（对于单语言 Hugo 站点是无害的）。

## 使用 `hugo new` 生成多语言内容 

If you organize content with translations in the same directory:

如果您将内容与翻译组织在同一个目录中：

```text
hugo new post/test.en.md
hugo new post/test.de.md
```

If you organize content with translations in different directories:

如果您将翻译后的内容组织在不同的目录中：

```text
hugo new content/en/post/test.md
hugo new content/de/post/test.md
```

## 另请参阅 

- [i18n](https://gohugo.io/functions/i18n/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [relLangURL](https://gohugo.io/functions/rellangurl/)
- [uniq](https://gohugo.io/functions/uniq/)
- [0.65.0: Hugo Reloaded!](https://gohugo.io/news/0.65.0-relnotes/)
