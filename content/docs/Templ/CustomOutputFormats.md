+++
title = "自定义输出格式"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Custom Output Formats - 自定义输出格式 

[https://gohugo.io/templates/output-formats/](https://gohugo.io/templates/output-formats/)

​	Hugo可以将内容输出为多种格式，包括日历事件、电子书格式、Google AMP和JSON搜索索引，或任何自定义文本格式。 

​	本页介绍了如何正确配置站点的媒体类型和输出格式，以及如何为自定义输出创建模板。

## 媒体类型 

​	[媒体类型](https://en.wikipedia.org/wiki/Media_type)（也称为MIME类型和内容类型）是用于在互联网上传输文件格式和格式内容的两部分标识符。

​	这是Hugo中的完整内置媒体类型集：

| type                      | suffixes                |
| :------------------------ | :---------------------- |
| application/json          | [json]                  |
| application/manifest+json | [webmanifest]           |
| application/octet-stream  | []                      |
| application/pdf           | [pdf]                   |
| application/rss+xml       | [xml rss]               |
| application/toml          | [toml]                  |
| application/xml           | [xml]                   |
| application/yaml          | [yaml yml]              |
| font/otf                  | [otf]                   |
| font/ttf                  | [ttf]                   |
| image/bmp                 | [bmp]                   |
| image/gif                 | [gif]                   |
| image/jpeg                | [jpg jpeg jpe jif jfif] |
| image/png                 | [png]                   |
| image/svg+xml             | [svg]                   |
| image/webp                | [webp]                  |
| text/calendar             | [ics]                   |
| text/css                  | [css]                   |
| text/csv                  | [csv]                   |
| text/html                 | [html]                  |
| text/javascript           | [js jsm mjs]            |
| text/jsx                  | [jsx]                   |
| text/markdown             | [md markdown]           |
| text/plain                | [txt]                   |
| text/tsx                  | [tsx]                   |
| text/typescript           | [ts]                    |
| text/x-sass               | [sass]                  |
| text/x-scss               | [scss]                  |
| video/3gpp                | [3gpp 3gp]              |
| video/mp4                 | [mp4]                   |
| video/mpeg                | [mpg mpeg]              |
| video/ogg                 | [ogv]                   |
| video/webm                | [webm]                  |
| video/x-msvideo           | [avi]                   |

注意：

- 可以添加自定义媒体类型或更改默认值；例如，如果您想将`text/html`的后缀更改为`asp`。 
- `Suffixes`是在Hugo中用于该媒体类型的URL和文件名的值。 
- `Type`是定义新/自定义`Output Formats`时必须使用的标识符（见下文）。 
- 完整的媒体类型集将在Hugo的内置开发服务器中注册，以确保它们被浏览器识别。 

​	要添加或修改媒体类型，请在[站点配置](https://gohugo.io/getting-started/configuration/)中的`mediaTypes`部分中定义它，可以为所有站点或特定语言定义。

config.

=== "yaml"

    ``` yaml
    mediaTypes:
      text/enriched:
        suffixes:
        - enr
      text/html:
        suffixes:
        - asp
    ```

=== "toml"

    ``` toml
    [mediaTypes]
      [mediaTypes.'text/enriched']
        suffixes = ['enr']
      [mediaTypes.'text/html']
        suffixes = ['asp']
    ```

=== "json"

    ``` json
    {
       "mediaTypes": {
          "text/enriched": {
             "suffixes": [
                "enr"
             ]
          },
          "text/html": {
             "suffixes": [
                "asp"
             ]
          }
       }
    }
    ```



​	上面的示例添加了一个新的媒体类型`text/enriched`，并更改了内置的`text/html`媒体类型的后缀。

注意：这些媒体类型是针对您的输出格式进行配置的。如果要重新定义Hugo的默认输出格式（例如`HTML`），还需要重新定义媒体类型。因此，如果要将HTML输出格式的后缀从`html`（默认）更改为`htm`：

config.

=== "yaml"

    ``` yaml
    mediaTypes:
      text/html:
        suffixes:
        - htm
    outputFormats:
      HTML:
        mediaType: text/html
    ```

=== "toml"

    ``` toml
    [mediaTypes]
      [mediaTypes.'text/html']
        suffixes = ['htm']
    [outputFormats]
      [outputFormats.HTML]
        mediaType = 'text/html'
    ```

=== "json"

    ``` json
    {
       "mediaTypes": {
          "text/html": {
             "suffixes": [
                "htm"
             ]
          }
       },
       "outputFormats": {
          "HTML": {
             "mediaType": "text/html"
          }
       }
    }
    ```

注意，要让上述内容生效，您还需要在站点配置中添加 `outputs` 定义。

## 输出格式定义 

​	给定一个媒体类型和一些其他配置，您可以获得一个输出格式。

​	这是Hugo的所有内置输出格式：

| name           | mediaType                 | path | baseName | rel        | protocol  | isPlainText | isHTML | noUgly | permalinkable |
| :------------- | :------------------------ | :--- | :------- | :--------- | :-------- | :---------- | :----- | :----- | :------------ |
| HTML           | text/html                 |      | index    | canonical  |           | false       | true   | false  | true          |
| AMP            | text/html                 | amp  | index    | amphtml    |           | false       | true   | false  | true          |
| CSS            | text/css                  |      | styles   | stylesheet |           | true        | false  | false  | false         |
| CSV            | text/csv                  |      | index    | alternate  |           | true        | false  | false  | false         |
| Calendar       | text/calendar             |      | index    | alternate  | webcal:// | true        | false  | false  | false         |
| JSON           | application/json          |      | index    | alternate  |           | true        | false  | false  | false         |
| MARKDOWN       | text/markdown             |      | index    | alternate  |           | true        | false  | false  | false         |
| ROBOTS         | text/plain                |      | robots   | alternate  |           | true        | false  | false  | false         |
| RSS            | application/rss+xml       |      | index    | alternate  |           | false       | false  | true   | false         |
| Sitemap        | application/xml           |      | sitemap  | sitemap    |           | false       | false  | true   | false         |
| WebAppManifest | application/manifest+json |      | manifest | manifest   |           | true        | false  | false  | false         |

- 一个页面可以按您想要的多种输出格式输出，只要它们在文件系统上解析为唯一路径即可定义无限数量的输出格式。在上面的表格中，最好的例子是`AMP` vs `HTML`。`AMP`的`Path`值为`amp`，因此不会覆盖`HTML`版本。例如，我们现在可以同时拥有 `/index.html` 和 `/amp/index.html`。 
- `MediaType` 必须匹配已定义媒体类型的`Type`。
- 您可以定义新的输出格式或重新定义内置的输出格式；例如，如果您想将`AMP`页面放在不同的路径中。 

​	要添加或修改输出格式，请在站点[配置文件](https://gohugo.io/getting-started/configuration/)中的 `outputFormats` 部分中定义它，无论是为所有站点还是为给定的语言。

config.

=== "yaml"

    ``` yaml
    outputFormats:
      MyEnrichedFormat:
        baseName: myindex
        isPlainText: true
        mediaType: text/enriched
        protocol: bep://
    ```

=== "toml"

    ``` toml
    [outputFormats]
      [outputFormats.MyEnrichedFormat]
        baseName = 'myindex'
        isPlainText = true
        mediaType = 'text/enriched'
        protocol = 'bep://'
    ```

=== "json"

    ``` json
    {
       "outputFormats": {
          "MyEnrichedFormat": {
             "baseName": "myindex",
             "isPlainText": true,
             "mediaType": "text/enriched",
             "protocol": "bep://"
          }
       }
    }
    ```



​	上述示例是虚构的，但如果用于具有 `baseURL` `https://example.org` 的站点的主页，它将产生一个具有 URL `bep://example.org/myindex.enr` 的纯文本主页。

### 配置输出格式 

​	以下是输出格式的完整配置选项列表及其默认值：

- `name`

  输出格式标识符。用于定义您页面的输出格式。 

- `mediaType`

  这必须与已定义的媒体类型的`Type`匹配。 

- `path`

  保存输出文件的子路径。 

- `baseName`

  用于列表文件名（主页等）的基本文件名。默认值：`index`。 

- `rel`

  可用于在`link`标记中创建 `rel` 值。默认值：`alternate`。 

- `protocol`

  将替换 `baseURL` 中此输出格式的"http://"或"https://"。

- `isPlainText`

  使用 Go 的纯文本模板解析器进行模板解析。默认值： `false`。 

- `isHTML`

  仅在与 HTML 类型格式相关的情况下使用，例如页面别名。默认值： `false`。 

- `noUgly`

  用于关闭丑陋的 URL（如果在站点中设置了 `uglyURLs`为 `true`）。默认值： `false`。

- `notAlternative`

  enable if it doesn’t make sense to include this format in an `AlternativeOutputFormats` format listing on `Page` (e.g., with `CSS`). Note that we use the term *alternative* and not *alternate* here, as it does not necessarily replace the other format. **Default:** `false`.

  如果在`Page`的 `AlternativeOutputFormats` 格式列表中包含此格式不合理（例如使用 `CSS`），则启用此选项。请注意，此处我们使用 `alternative` 而不是 `alternate` 一词，因为它并不一定替代其他格式。默认值： `false`。

- `permalinkable`

  使 `.Permalink` 和 `.RelPermalink` 返回渲染输出格式而不是主格式（[见下文](https://gohugo.io/templates/output-formats/#link-to-output-formats)）。默认情况下，对于 `HTML` 和 `AMP` 启用此选项。默认值： `false`。 

- `weight`

  将其设置为非零值将用作第一个排序标准。

## 页面的输出格式 

​	在 Hugo 中，`Page`可以在文件系统上呈现为多种输出格式。

### 默认输出格式 

​	每个`Page`都有一个 `Kind` 属性，其默认输出格式是基于此属性设置的。

| Kind       | Default Output Formats |
| :--------- | :--------------------- |
| `page`     | HTML                   |
| `home`     | HTML, RSS              |
| `section`  | HTML, RSS              |
| `taxonomy` | HTML, RSS              |
| `term`     | HTML, RSS              |

### 自定义输出格式 

​	这可以通过在`Page`前置元数据或站点配置（对所有站点或每种语言）中定义一个`outputs`列表来更改。

​	站点配置文件中的示例：

config.

=== "yaml"

    ``` yaml
    outputs:
      home:
      - HTML
      - AMP
      - RSS
      page:
      - HTML
    ```

=== "toml"

    ``` toml
    [outputs]
      home = ['HTML', 'AMP', 'RSS']
      page = ['HTML']
    ```

=== "json"

    ``` json
    {
       "outputs": {
          "home": [
             "HTML",
             "AMP",
             "RSS"
          ],
          "page": [
             "HTML"
          ]
       }
    }
    ```



请注意，在上面的示例中，`section`、`taxonomy`和`term`的输出格式将保持其默认值 `["HTML", "RSS"]`。

| Kind       | Description                              | Example                                                      |
| :--------- | :--------------------------------------- | :----------------------------------------------------------- |
| `home`     | The landing page for the home page       | `/index.html`                                                |
| `page`     | The landing page for a given page        | `my-post` page (`/posts/my-post/index.html`)                 |
| `section`  | The landing page of a given section      | `posts` section (`/posts/index.html`)                        |
| `taxonomy` | The landing page for a taxonomy          | `tags` taxonomy (`/tags/index.html`)                         |
| `term`     | The landing page for one taxonomy’s term | term `awesome` in `tags` taxonomy (`/tags/awesome/index.html`) |

- `outputs` 定义是每种[`Page`的 `Kind`](https://gohugo.io/templates/section-templates/#page-kinds)（`page`、`home`、`section`、`taxonomy` 或 `term`）的。 

- These can be overridden per `Page` in the front matter of content files.

- 所使用的名称（例如 `HTML`、`AMP`）必须与已定义的输出格式的`Name`匹配。

  这些名称不区分大小写。 
- 这些可以在内容文件的前置元数据中针对每个`Page`进行覆盖。

  

​	以下是一个在内容文件中定义呈现`Page`输出格式的前置元数据的示例：

content/example.md

=== "yaml"

    ``` yaml
    ---
    outputs:
    - html
    - amp
    - json
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    outputs = ['html', 'amp', 'json']
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "outputs": [
          "html",
          "amp",
          "json"
       ],
       "title": "Example"
    }
    ```



## 输出格式列表 

​	每个`Page`都有 `.OutputFormats`（所有格式，包括当前格式）和 `.AlternativeOutputFormats` 变量，后者可用于在站点的 `<head>` 中创建`link rel` 列表。

```go-html-template
{{ range .AlternativeOutputFormats -}}
<link rel="{{ .Rel }}" type="{{ .MediaType.Type }}" href="{{ .Permalink | safeURL }}">
{{ end -}}
```

## 输出格式链接 

​	`Page` 上的 `.Permalink` 和 `.RelPermalink` 将返回为该页面定义的第一个输出格式（通常为 `HTML`，如果没有其他定义的话）。这与调用它们的模板文件无关。

来自 `single.json.json`：

```go-html-template
{{ .RelPermalink }} > /that-page/
{{ with  .OutputFormats.Get "json" -}}
{{ .RelPermalink }} > /that-page/index.json
{{- end }}
```

​	为了使它们返回当前模板文件的输出格式，给定的输出格式应设置其 `permalinkable` 属性为 `true`。

与上面相同的模板文件，带有json 输出格式的 `permalinkable` 设置为 true：

```go-html-template
{{ .RelPermalink }} > /that-page/index.json
{{ with  .OutputFormats.Get "html" -}}
{{ .RelPermalink }} > /that-page/
{{- end }}
```

​	从内容文件中，您可以使用 [`ref` 或 `relref` 简码](https://gohugo.io/content-management/shortcodes/#ref-and-relref)：

```go-html-template
[Neat](\{\{\< ref "blog/neat.md" "amp" \>\}\})
[Who](\{\{\< relref "about.md#who" "amp" \>\}\})
```

## 您的输出格式模板 

​	一个新的输出格式需要一个相应的模板才能渲染任何有用的内容。

​	对于 Hugo 0.20 及更高版本的关键区别在于，Hugo 查看输出格式的 `Name` 和 MediaType 的 `Suffixes`，以选择用于渲染给定 `Page` 的模板。

​	以下表格显示了不同输出格式的示例、所使用的后缀以及 Hugo 的模板[查找顺序](https://gohugo.io/templates/lookup-order/)。表格中的所有示例都可以：

- 使用[基础模板](https://gohugo.io/templates/base/)。 
- 包含[局部模板](https://gohugo.io/templates/partials/)。

| Example                                                      | OutputFormat | Suffix | Template Lookup Order                                        |
| :----------------------------------------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| "posts" 章节的单个页面                                       | HTML         | html   | [layouts/posts/single.html.html layouts/posts/single.html layouts/_default/single.html.html layouts/_default/single.html] |
| "posts" 章节的单个页面基础模板                               | HTML         | html   | [layouts/posts/single-baseof.html.html layouts/posts/baseof.html.html layouts/posts/single-baseof.html layouts/posts/baseof.html layouts/_default/single-baseof.html.html layouts/_default/baseof.html.html layouts/_default/single-baseof.html layouts/_default/baseof.html] |
| Single page in "posts" section with layout set               | HTML         | html   | [layouts/posts/demolayout.html.html layouts/posts/single.html.html layouts/posts/demolayout.html layouts/posts/single.html layouts/_default/demolayout.html.html layouts/_default/single.html.html layouts/_default/demolayout.html layouts/_default/single.html] |
| Base template for single page in "posts" section with layout set | HTML         | html   | [layouts/posts/demolayout-baseof.html.html layouts/posts/single-baseof.html.html layouts/posts/baseof.html.html layouts/posts/demolayout-baseof.html layouts/posts/single-baseof.html layouts/posts/baseof.html layouts/_default/demolayout-baseof.html.html layouts/_default/single-baseof.html.html layouts/_default/baseof.html.html layouts/_default/demolayout-baseof.html layouts/_default/single-baseof.html layouts/_default/baseof.html] |
| AMP single page                                              | AMP          | html   | [layouts/posts/single.amp.html layouts/posts/single.html layouts/_default/single.amp.html layouts/_default/single.html] |
| AMP single page, French language                             | AMP          | html   | [layouts/posts/single.fr.amp.html layouts/posts/single.amp.html layouts/posts/single.fr.html layouts/posts/single.html layouts/_default/single.fr.amp.html layouts/_default/single.amp.html layouts/_default/single.fr.html layouts/_default/single.html] |
| Home page                                                    | HTML         | html   | [layouts/index.html.html layouts/home.html.html layouts/list.html.html layouts/index.html layouts/home.html layouts/list.html layouts/_default/index.html.html layouts/_default/home.html.html layouts/_default/list.html.html layouts/_default/index.html layouts/_default/home.html layouts/_default/list.html] |
| Base template for home page                                  | HTML         | html   | [layouts/index-baseof.html.html layouts/home-baseof.html.html layouts/list-baseof.html.html layouts/baseof.html.html layouts/index-baseof.html layouts/home-baseof.html layouts/list-baseof.html layouts/baseof.html layouts/_default/index-baseof.html.html layouts/_default/home-baseof.html.html layouts/_default/list-baseof.html.html layouts/_default/baseof.html.html layouts/_default/index-baseof.html layouts/_default/home-baseof.html layouts/_default/list-baseof.html layouts/_default/baseof.html] |
| Home page with type set                                      | HTML         | html   | [layouts/demotype/index.html.html layouts/demotype/home.html.html layouts/demotype/list.html.html layouts/demotype/index.html layouts/demotype/home.html layouts/demotype/list.html layouts/index.html.html layouts/home.html.html layouts/list.html.html layouts/index.html layouts/home.html layouts/list.html layouts/_default/index.html.html layouts/_default/home.html.html layouts/_default/list.html.html layouts/_default/index.html layouts/_default/home.html layouts/_default/list.html] |
| Base template for home page with type set                    | HTML         | html   | [layouts/demotype/index-baseof.html.html layouts/demotype/home-baseof.html.html layouts/demotype/list-baseof.html.html layouts/demotype/baseof.html.html layouts/demotype/index-baseof.html layouts/demotype/home-baseof.html layouts/demotype/list-baseof.html layouts/demotype/baseof.html layouts/index-baseof.html.html layouts/home-baseof.html.html layouts/list-baseof.html.html layouts/baseof.html.html layouts/index-baseof.html layouts/home-baseof.html layouts/list-baseof.html layouts/baseof.html layouts/_default/index-baseof.html.html layouts/_default/home-baseof.html.html layouts/_default/list-baseof.html.html layouts/_default/baseof.html.html layouts/_default/index-baseof.html layouts/_default/home-baseof.html layouts/_default/list-baseof.html layouts/_default/baseof.html] |
| Home page with layout set                                    | HTML         | html   | [layouts/demolayout.html.html layouts/index.html.html layouts/home.html.html layouts/list.html.html layouts/demolayout.html layouts/index.html layouts/home.html layouts/list.html layouts/_default/demolayout.html.html layouts/_default/index.html.html layouts/_default/home.html.html layouts/_default/list.html.html layouts/_default/demolayout.html layouts/_default/index.html layouts/_default/home.html layouts/_default/list.html] |
| AMP home, French language                                    | AMP          | html   | [layouts/index.fr.amp.html layouts/home.fr.amp.html layouts/list.fr.amp.html layouts/index.amp.html layouts/home.amp.html layouts/list.amp.html layouts/index.fr.html layouts/home.fr.html layouts/list.fr.html layouts/index.html layouts/home.html layouts/list.html layouts/_default/index.fr.amp.html layouts/_default/home.fr.amp.html layouts/_default/list.fr.amp.html layouts/_default/index.amp.html layouts/_default/home.amp.html layouts/_default/list.amp.html layouts/_default/index.fr.html layouts/_default/home.fr.html layouts/_default/list.fr.html layouts/_default/index.html layouts/_default/home.html layouts/_default/list.html] |
| JSON home                                                    | JSON         | json   | [layouts/index.json.json layouts/home.json.json layouts/list.json.json layouts/index.json layouts/home.json layouts/list.json layouts/_default/index.json.json layouts/_default/home.json.json layouts/_default/list.json.json layouts/_default/index.json layouts/_default/home.json layouts/_default/list.json] |
| RSS home                                                     | RSS          | xml    | [layouts/index.rss.xml layouts/home.rss.xml layouts/rss.xml layouts/list.rss.xml layouts/index.xml layouts/home.xml layouts/list.xml layouts/_default/index.rss.xml layouts/_default/home.rss.xml layouts/_default/rss.xml layouts/_default/list.rss.xml layouts/_default/index.xml layouts/_default/home.xml layouts/_default/list.xml layouts/_internal/_default/rss.xml] |
| RSS section posts                                            | RSS          | xml    | [layouts/posts/section.rss.xml layouts/posts/rss.xml layouts/posts/list.rss.xml layouts/posts/section.xml layouts/posts/list.xml layouts/section/section.rss.xml layouts/section/rss.xml layouts/section/list.rss.xml layouts/section/section.xml layouts/section/list.xml layouts/_default/section.rss.xml layouts/_default/rss.xml layouts/_default/list.rss.xml layouts/_default/section.xml layouts/_default/list.xml layouts/_internal/_default/rss.xml] |
| Taxonomy in categories                                       | RSS          | xml    | [layouts/categories/category.terms.rss.xml layouts/categories/terms.rss.xml layouts/categories/taxonomy.rss.xml layouts/categories/rss.xml layouts/categories/list.rss.xml layouts/categories/category.terms.xml layouts/categories/terms.xml layouts/categories/taxonomy.xml layouts/categories/list.xml layouts/category/category.terms.rss.xml layouts/category/terms.rss.xml layouts/category/taxonomy.rss.xml layouts/category/rss.xml layouts/category/list.rss.xml layouts/category/category.terms.xml layouts/category/terms.xml layouts/category/taxonomy.xml layouts/category/list.xml layouts/taxonomy/category.terms.rss.xml layouts/taxonomy/terms.rss.xml layouts/taxonomy/taxonomy.rss.xml layouts/taxonomy/rss.xml layouts/taxonomy/list.rss.xml layouts/taxonomy/category.terms.xml layouts/taxonomy/terms.xml layouts/taxonomy/taxonomy.xml layouts/taxonomy/list.xml layouts/_default/category.terms.rss.xml layouts/_default/terms.rss.xml layouts/_default/taxonomy.rss.xml layouts/_default/rss.xml layouts/_default/list.rss.xml layouts/_default/category.terms.xml layouts/_default/terms.xml layouts/_default/taxonomy.xml layouts/_default/list.xml layouts/_internal/_default/rss.xml] |
| Term in categories                                           | RSS          | xml    | [layouts/categories/term.rss.xml layouts/categories/category.rss.xml layouts/categories/taxonomy.rss.xml layouts/categories/rss.xml layouts/categories/list.rss.xml layouts/categories/term.xml layouts/categories/category.xml layouts/categories/taxonomy.xml layouts/categories/list.xml layouts/term/term.rss.xml layouts/term/category.rss.xml layouts/term/taxonomy.rss.xml layouts/term/rss.xml layouts/term/list.rss.xml layouts/term/term.xml layouts/term/category.xml layouts/term/taxonomy.xml layouts/term/list.xml layouts/taxonomy/term.rss.xml layouts/taxonomy/category.rss.xml layouts/taxonomy/taxonomy.rss.xml layouts/taxonomy/rss.xml layouts/taxonomy/list.rss.xml layouts/taxonomy/term.xml layouts/taxonomy/category.xml layouts/taxonomy/taxonomy.xml layouts/taxonomy/list.xml layouts/category/term.rss.xml layouts/category/category.rss.xml layouts/category/taxonomy.rss.xml layouts/category/rss.xml layouts/category/list.rss.xml layouts/category/term.xml layouts/category/category.xml layouts/category/taxonomy.xml layouts/category/list.xml layouts/_default/term.rss.xml layouts/_default/category.rss.xml layouts/_default/taxonomy.rss.xml layouts/_default/rss.xml layouts/_default/list.rss.xml layouts/_default/term.xml layouts/_default/category.xml layouts/_default/taxonomy.xml layouts/_default/list.xml layouts/_internal/_default/rss.xml] |
| Section list for "posts" section                             | HTML         | html   | [layouts/posts/posts.html.html layouts/posts/section.html.html layouts/posts/list.html.html layouts/posts/posts.html layouts/posts/section.html layouts/posts/list.html layouts/section/posts.html.html layouts/section/section.html.html layouts/section/list.html.html layouts/section/posts.html layouts/section/section.html layouts/section/list.html layouts/_default/posts.html.html layouts/_default/section.html.html layouts/_default/list.html.html layouts/_default/posts.html layouts/_default/section.html layouts/_default/list.html] |
| Section list for "posts" section with type set to "blog"     | HTML         | html   | [layouts/blog/posts.html.html layouts/blog/section.html.html layouts/blog/list.html.html layouts/blog/posts.html layouts/blog/section.html layouts/blog/list.html layouts/posts/posts.html.html layouts/posts/section.html.html layouts/posts/list.html.html layouts/posts/posts.html layouts/posts/section.html layouts/posts/list.html layouts/section/posts.html.html layouts/section/section.html.html layouts/section/list.html.html layouts/section/posts.html layouts/section/section.html layouts/section/list.html layouts/_default/posts.html.html layouts/_default/section.html.html layouts/_default/list.html.html layouts/_default/posts.html layouts/_default/section.html layouts/_default/list.html] |
| Section list for "posts" section with layout set to "demoLayout" | HTML         | html   | [layouts/posts/demolayout.html.html layouts/posts/posts.html.html layouts/posts/section.html.html layouts/posts/list.html.html layouts/posts/demolayout.html layouts/posts/posts.html layouts/posts/section.html layouts/posts/list.html layouts/section/demolayout.html.html layouts/section/posts.html.html layouts/section/section.html.html layouts/section/list.html.html layouts/section/demolayout.html layouts/section/posts.html layouts/section/section.html layouts/section/list.html layouts/_default/demolayout.html.html layouts/_default/posts.html.html layouts/_default/section.html.html layouts/_default/list.html.html layouts/_default/demolayout.html layouts/_default/posts.html layouts/_default/section.html layouts/_default/list.html] |
| Taxonomy list in categories                                  | HTML         | html   | [layouts/categories/category.terms.html.html layouts/categories/terms.html.html layouts/categories/taxonomy.html.html layouts/categories/list.html.html layouts/categories/category.terms.html layouts/categories/terms.html layouts/categories/taxonomy.html layouts/categories/list.html layouts/category/category.terms.html.html layouts/category/terms.html.html layouts/category/taxonomy.html.html layouts/category/list.html.html layouts/category/category.terms.html layouts/category/terms.html layouts/category/taxonomy.html layouts/category/list.html layouts/taxonomy/category.terms.html.html layouts/taxonomy/terms.html.html layouts/taxonomy/taxonomy.html.html layouts/taxonomy/list.html.html layouts/taxonomy/category.terms.html layouts/taxonomy/terms.html layouts/taxonomy/taxonomy.html layouts/taxonomy/list.html layouts/_default/category.terms.html.html layouts/_default/terms.html.html layouts/_default/taxonomy.html.html layouts/_default/list.html.html layouts/_default/category.terms.html layouts/_default/terms.html layouts/_default/taxonomy.html layouts/_default/list.html] |
| Taxonomy term in categories                                  | HTML         | html   | [layouts/categories/term.html.html layouts/categories/category.html.html layouts/categories/taxonomy.html.html layouts/categories/list.html.html layouts/categories/term.html layouts/categories/category.html layouts/categories/taxonomy.html layouts/categories/list.html layouts/term/term.html.html layouts/term/category.html.html layouts/term/taxonomy.html.html layouts/term/list.html.html layouts/term/term.html layouts/term/category.html layouts/term/taxonomy.html layouts/term/list.html layouts/taxonomy/term.html.html layouts/taxonomy/category.html.html layouts/taxonomy/taxonomy.html.html layouts/taxonomy/list.html.html layouts/taxonomy/term.html layouts/taxonomy/category.html layouts/taxonomy/taxonomy.html layouts/taxonomy/list.html layouts/category/term.html.html layouts/category/category.html.html layouts/category/taxonomy.html.html layouts/category/list.html.html layouts/category/term.html layouts/category/category.html layouts/category/taxonomy.html layouts/category/list.html layouts/_default/term.html.html layouts/_default/category.html.html layouts/_default/taxonomy.html.html layouts/_default/list.html.html layouts/_default/term.html layouts/_default/category.html layouts/_default/taxonomy.html layouts/_default/list.html] |

​	Hugo 现在还可以检测 partials 的媒体类型和输出格式（如果可能的话），并使用这些信息来决定是否将 partial 解析为纯文本模板。

​	Hugo将查找给定的名称，因此您可以根据需要随意命名它。但是，如果要将其视为纯文本，请使用文件后缀，如果需要，还要使用输出格式的名称。 模式如下：

```go-html-template
[partial name].[OutputFormat].[suffix]
```

​	以下 partial 是一个纯文本模板（输出格式为 `CSV`，由于这是唯一带有后缀 `csv` 的输出格式，因此我们不需要包含输出格式的`Name`）：

```go-html-template
{{ partial "mytextpartial.csv" . }}
```

## 另请参阅 

- [Hugo中的内容列表 ](https://gohugo.io/templates/lists/)
- [RSS模板](https://gohugo.io/templates/rss/)
