+++
title = "数据模板"
weight = 12
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Data Templates - 数据模板 

[https://gohugo.io/templates/data-templates/](https://gohugo.io/templates/data-templates/)

​	除了Hugo内置的变量，您可以在模板或简码中指定自己的自定义数据，这些数据可以来自本地和动态源。 

​	Hugo支持从位于Hugo项目根目录下的`data`目录中的YAML、JSON、XML和TOML文件加载数据。

<iframe src="https://www.youtube.com/embed/FyPgSuwIMWQ" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

## data文件夹 

​	`data` 文件夹应该存储在生成站点时 Hugo 需要使用的其他数据。

​	数据文件不用于生成独立的页面。它们应该通过以下方式补充内容文件： 

- 当前置元数据字段过于复杂时扩展内容；或 
- 在模板中显示一个更大的数据集（参见下面的示例）

​	在这两种情况下，最好将这些数据外包到它们（自己的）的文件中。

​	这些文件必须是 YAML、JSON、XML 或 TOML 文件（使用 `.yml`、`.yaml`、`.json`、`.xml` 或 `.toml` 扩展名）。这些数据将作为 `map` 存储在 `.Site.Data` 变量中。

​	要使用 `site.Data.filename` 表示法访问数据，该filename必须以下划线或 Unicode 字母开头，后跟零个或多个下划线、Unicode 字母或 Unicode 数字。例如：

- `123.json` - 无效的
- `x123.json` - 有效的
- `_123.json` - 有效的

​	要使用 [index](https://gohugo.io/functions/index-function/) 函数访问这些数据，则该文件名无关紧要。例如：

| 数据文件     | 模板代码                         |
| :----------- | :------------------------------- |
| `123.json`   | `{{ index .Site.Data "123" }}`   |
| `x123.json`  | `{{ index .Site.Data "x123" }}`  |
| `_123.json`  | `{{ index .Site.Data "_123" }}`  |
| `x-123.json` | `{{ index .Site.Data "x-123" }}` |

## 主题中的数据文件 

​	数据文件也可以在主题中使用。

​	但是，请注意，主题数据文件与项目目录合并，以项目目录为优先。也就是说，如果存在相同名称和相对路径的两个文件，则根项目 `data` 目录中文件中的数据将覆盖 `themes/<THEME>/data` 目录中文件中的数据（对于重复的键）。

​	因此，主题作者应该小心，不要包含用户可以轻松覆盖的数据文件，因为用户可能决定[自定义主题](https://gohugo.io/hugo-modules/theme-components/)。对于不应被覆盖的特定于主题的数据项，最好在文件夹结构前加上命名空间，例如 `mytheme/data/<THEME>/somekey/...`。要检查是否存在此类重复项，请使用 `-v` 标志运行 hugo。

​	从数据文件创建数据模板的映射中的键将是一组点链接的 `path`、`filename` 和文件中的 `key`（如果适用）。

​	以下是最好的说明例子：

## 示例：Jaco Pastorius的个人唱片 

​	[Jaco Pastorius](https://en.wikipedia.org/wiki/Jaco_Pastorius_discography) 是一位伟大的贝斯手，但他的个人唱片分类目录非常简短，足以作为一个示例。[John Patitucci](https://en.wikipedia.org/wiki/John_Patitucci) 是另一位贝斯巨匠。

​	下面的示例有点牵强，但它说明了数据文件的灵活性。这个示例使用 TOML 作为文件格式，其中包含以下两个数据文件：

- `data/jazz/bass/jacopastorius.toml`
- `data/jazz/bass/johnpatitucci.toml`

​	`jacopastorius.toml` 包含以下内容。 `johnpatitucci.toml` 包含类似的列表：

jacopastorius.

=== "yaml"

    ``` yaml
    discography:
    - 1974 - Modern American Music … Period! The Criteria Sessions
    - 1974 - Jaco
    - 1976 - Jaco Pastorius
    - 1981 - Word of Mouth
    - 1981 - The Birthday Concert (released in 1995)
    - 1982 - Twins I & II (released in 1999)
    - 1983 - Invitation
    - 1986 - Broadway Blues (released in 1998)
    - 1986 - Honestly Solo Live (released in 1990)
    - 1986 - Live In Italy (released in 1991)
    - 1986 - Heavy'n Jazz (released in 1992)
    - 1991 - Live In New York City, Volumes 1-7.
    - 1999 - Rare Collection (compilation)
    - '2003 - Punk Jazz: The Jaco Pastorius Anthology (compilation)'
    - 2007 - The Essential Jaco Pastorius (compilation)
    ```

=== "toml"

    ``` toml
    discography = ['1974 - Modern American Music … Period! The Criteria Sessions', '1974 - Jaco', '1976 - Jaco Pastorius', '1981 - Word of Mouth', '1981 - The Birthday Concert (released in 1995)', '1982 - Twins I & II (released in 1999)', '1983 - Invitation', '1986 - Broadway Blues (released in 1998)', '1986 - Honestly Solo Live (released in 1990)', '1986 - Live In Italy (released in 1991)', "1986 - Heavy'n Jazz (released in 1992)", '1991 - Live In New York City, Volumes 1-7.', '1999 - Rare Collection (compilation)', '2003 - Punk Jazz: The Jaco Pastorius Anthology (compilation)', '2007 - The Essential Jaco Pastorius (compilation)']
    ```

=== "json"

    ``` json
    {
       "discography": [
          "1974 - Modern American Music … Period! The Criteria Sessions",
          "1974 - Jaco",
          "1976 - Jaco Pastorius",
          "1981 - Word of Mouth",
          "1981 - The Birthday Concert (released in 1995)",
          "1982 - Twins I \u0026 II (released in 1999)",
          "1983 - Invitation",
          "1986 - Broadway Blues (released in 1998)",
          "1986 - Honestly Solo Live (released in 1990)",
          "1986 - Live In Italy (released in 1991)",
          "1986 - Heavy'n Jazz (released in 1992)",
          "1991 - Live In New York City, Volumes 1-7.",
          "1999 - Rare Collection (compilation)",
          "2003 - Punk Jazz: The Jaco Pastorius Anthology (compilation)",
          "2007 - The Essential Jaco Pastorius (compilation)"
       ]
    }
    ```



​	可以通过 `.Site.Data.jazz.bass` 访问贝斯手列表，通过添加文件名而不带后缀名来访问单个贝斯手，例如 `.Site.Data.jazz.bass.jacopastorius`。

​	现在可以在模板中呈现所有贝斯手的唱片列表：

```go-html-template
{{ range $.Site.Data.jazz.bass }}
   {{ partial "artist.html" . }}
{{ end }}
```

​	然后在 `partials/artist.html` 中：

```go-html-template
<ul>
{{ range .discography }}
  <li>{{ . }}</li>
{{ end }}
</ul>
```

​	发现新的喜欢的贝斯手？只需在相同的目录中添加另一个 `.toml` 文件即可。

## 示例：从数据文件中访问命名的值 

​	假设在 `data/` 下的 `User0123.[yml|toml|xml|json]` 数据文件中，您有以下数据结构：

User0123.

=== "yaml"

    ``` yaml
    Achievements:
    - Can create a Key, Value list from Data File
    - Learns Hugo
    - Reads documentation
    Name: User0123
    Short Description: He is a **jolly good** fellow.
    ```

=== "toml"

    ``` toml
    Achievements = ['Can create a Key, Value list from Data File', 'Learns Hugo', 'Reads documentation']
    Name = 'User0123'
    'Short Description' = 'He is a **jolly good** fellow.'
    ```

=== "json"

    ``` json
    {
       "Achievements": [
          "Can create a Key, Value list from Data File",
          "Learns Hugo",
          "Reads documentation"
       ],
       "Name": "User0123",
       "Short Description": "He is a **jolly good** fellow."
    }
    ```



​	您可以使用以下代码在布局中渲染 `Short Description`：

```go-html-template
<div>Short Description of {{ .Site.Data.User0123.Name }}: <p>{{ index .Site.Data.User0123 "Short Description" | markdownify }}</p></div>
```

​	请注意使用 [`markdownify` 模板函数](https://gohugo.io/functions/markdownify/)。这将通过 Markdown 渲染引擎发送描述。

## 获取远程数据 

​	使用 `getJSON` 或 `getCSV` 获取远程数据：

```go-html-template
{{ $dataJ := getJSON "url" }}
{{ $dataC := getCSV "separator" "url" }}
```

​	如果为 URL 使用前缀或后缀，则这些函数接受[可变参数](https://en.wikipedia.org/wiki/Variadic_function)：

```go-html-template
{{ $dataJ := getJSON "url prefix" "arg1" "arg2" "arg n" }}
{{ $dataC := getCSV  "separator" "url prefix" "arg1" "arg2" "arg n" }}
```

​	`getCSV` 的分隔符（separator）必须放在第一个位置，并且只能是一个字符长。

​	所有传递的参数将连接到最终 URL：

```go-html-template
{{ $urlPre := "https://api.github.com" }}
{{ $gistJ := getJSON $urlPre "/users/GITHUB_USERNAME/gists" }}
```

​	这将在内部解析为以下内容：

```go-html-template
{{ $gistJ := getJSON "https://api.github.com/users/GITHUB_USERNAME/gists" }}
```

### 添加 HTTP 标头 

​	`getJSON` 和 `getCSV` 都以可选的 map 作为最后一个参数，例如：

```go-html-template
{{ $data := getJSON "https://example.org/api" (dict "Authorization" "Bearer abcd") }}
```

​	如果您需要同一标头键的多个值，请使用切片：

```go-html-template
{{ $data := getJSON "https://example.org/api" (dict "X-List" (slice "a" "b" "c")) }}
```

### CSV 文件示例 

​	对于`getCSV`，一个字符长的分隔符必须放在第一个位置，然后是URL。以下是从已发布的CSV在[partial模板](https://gohugo.io/templates/partials/)中创建HTML表格的示例：

layouts/partials/get-csv.html

```go-html-template
  <table>
    <thead>
      <tr>
      <th>Name</th>
      <th>Position</th>
      <th>Salary</th>
      </tr>
    </thead>
    <tbody>
    {{ $url := "https://example.com/finance/employee-salaries.csv" }}
    {{ $sep := "," }}
    {{ range $i, $r := getCSV $sep $url }}
      <tr>
        <td>{{ index $r 0 }}</td>
        <td>{{ index $r 1 }}</td>
        <td>{{ index $r 2 }}</td>
      </tr>
    {{ end }}
    </tbody>
  </table>
```

​	表达式`{{ index $r number }}`必须用于输出当前行的第n列。

### 缓存 URL 

​	每个下载的URL将被缓存到默认文件夹`$TMPDIR/hugo_cache/`中。变量`$TMPDIR`将被解析为依赖于您系统的临时目录。

​	使用命令行标志`--cacheDir`，您可以指定系统上的任何文件夹作为缓存目录。

​	您还可以在[主配置文件](https://gohugo.io/getting-started/configuration/)中设置`cacheDir`。

​	如果您不喜欢缓存，可以使用命令行标志`--ignoreCache`完全禁用缓存。

### 使用 REST URL 进行身份验证 

​	目前，您只能使用可以放入URL中的那些身份验证方法。[OAuth](https://en.wikipedia.org/wiki/OAuth)和其他身份验证方法未实现。

## 加载本地文件 

​	要使用`getJSON`和`getCSV`加载本地文件，源文件必须位于Hugo的工作目录中。文件扩展名不重要，但（文件的）内容重要。

​	它应用了与上面在[获取远程数据](https://gohugo.io/templates/data-templates/#get-remote-data)中相同的输出逻辑。

​	要使用`getCSV`加载的本地CSV文件必须位于`data`目录**之外**。

## 数据文件的 LiveReload 

​	当URL的内容发生更改时，没有机会触发[LiveReload](https://gohugo.io/getting-started/usage/#livereload)。但是，当*本地*文件更改时（即，`data/*`和`themes/<THEME>/data/*`），将触发LiveReload。不支持符号链接。请注意，由于下载数据需要一段时间，Hugo会在数据下载完成之前停止处理Markdown文件。

​	如果更改了任何本地文件并触发了LiveReload，则Hugo将从缓存中读取数据驱动（URL）内容。如果您禁用了缓存（例如，通过使用`hugo server --ignoreCache`运行服务器），Hugo将在每次LiveReload触发时重新下载内容。这可能会产生*巨大的*流量。您可能会很快达到API限制。

## 数据驱动内容的示例 

- 照片库采用 JSON 数据驱动：[https://github.com/pcdummy/hugo-lightslider-example](https://github.com/pcdummy/hugo-lightslider-example) 
- 使用数据驱动内容和自定义简码，在一篇文章中介绍了 GitHub 星标仓库：[GitHub Starred Repositories](https://github.com/SchumacherFM/blog-cs/blob/master/content%2Fposts%2Fgithub-starred.md)。

## 数据格式规范 

- [TOML 规范](https://github.com/toml-lang/toml)
- [YAML 规范](https://yaml.org/spec/)
- [JSON 规范](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)
- [CSV 规范](https://tools.ietf.org/html/rfc4180)
- [XML 规范](https://www.w3.org/XML/)

## 另请参阅

- [配置 Hugo](https://gohugo.io/getting-started/configuration/)
- [前置元数据](https://gohugo.io/content-management/front-matter/)
- [RSS 模板 ](https://gohugo.io/templates/rss/)
- [Sitemap模板](https://gohugo.io/templates/sitemap-template/)
- [jsonify](https://gohugo.io/functions/jsonify/)
