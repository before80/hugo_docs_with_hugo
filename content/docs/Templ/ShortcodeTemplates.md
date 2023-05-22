+++
title = "创建自己的简码"
weight = 14
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Create Your Own Shortcodes - 创建自己的简码

[https://gohugo.io/templates/shortcode-templates/](https://gohugo.io/templates/shortcode-templates/)

​	您可以使用与单页和列表页相同的模板语法来创建自己的简码，以扩展Hugo内置的简码。

​	简码是一种将模板合并成小型、可重用的代码片段的方式，您可以直接在内容中嵌入这些代码片段。从这个意义上说，您可以将简码视为[页面和列表模板](https://gohugo.io/templates/)与[基本内容文件](https://gohugo.io/content-management/formats/)之间的中间件。

​	Hugo还提供了常见用例的内置简码。（参见[内容管理：简码](https://gohugo.io/content-management/shortcodes/)。）

## 创建自定义Shortcodes 

​	Hugo的内置简码涵盖了许多常见但不是全部的用例。幸运的是，Hugo提供了轻松创建自定义简码以满足您站点需求的功能。

<iframe src="https://www.youtube.com/embed/Eu4zSaKOY4A" allowfullscreen="" title="YouTube Video" style="top: 0px; left: 0px; width: 543.991px; height: 305.994px; border: 0px;"></iframe>

### 文件位置 

​	要创建一个简码，请在 [源文件组织](https://gohugo.io/getting-started/directory-structure/#directory-structure-explained) 的 `layouts/shortcodes` 目录中放置一个 HTML 模板。请仔细考虑文件名，因为简码名称将与文件名相同，但没有 `.html` 扩展名。例如，`layouts/shortcodes/myshortcode.html` 将根据您选择的参数类型使用 `\{\{\< myshortcode /\>\}\}` 或 `\{\{\% myshortcode \/\%\}\}` 进行调用。

​	您可以在子文件夹中组织您的简码，例如在 `layouts/shortcodes/boxes` 中。然后，这些简码将使用它们的相对路径进行访问，例如：

```go-html-template
\{{\< boxes/square \>\}\}
```

​	注意正斜杠。

### 简码模板查找顺序 

​	简码模板具有简单的[查找顺序](https://gohugo.io/templates/lookup-order/)：

1. `/layouts/shortcodes/<SHORTCODE>.html`
2. `/themes/<THEME>/layouts/shortcodes/<SHORTCODE>.html`

### 位置参数 vs 命名参数 

​	您可以使用以下类型的参数创建简码：

- 位置参数 
- 命名参数 
- 位置或命名参数（即"灵活（flexible）"） 

​	在具有位置参数的简码中，参数的顺序很重要。如果简码有一个必需的单一值（例如下面的`youtube`简码），则位置参数非常有效，并且需要的内容作者输入较少。

​	对于具有多个或可选参数的更复杂的布局，命名参数效果最好。虽然不太简洁，但命名参数需要较少的内容作者记忆，并且可以按任意顺序添加到简码声明中。

​	允许两种类型的参数（即"灵活（flexible）"的简码）对于复杂的布局非常有用，您可以设置默认值，这些默认值可以很容易地被用户覆盖。

### 访问参数 

​	可以通过 `.Get` 方法访问所有简码参数。无论是将键（即字符串）还是数字传递给 `.Get` 方法取决于您是否正在访问命名或位置参数。

​	要通过名称访问参数，请使用`.Get`方法，后跟命名参数作为引用字符串的形式：

```go-html-template
{{ .Get "class" }}
```

​	要通过位置访问参数，请使用 `.Get`，后跟数字位置，要记住位置参数是从零开始编号的：

```go-html-template
{{ .Get 0 }}
```

​	对于第二个位置，您只需要使用：

```go-html-template
{{ .Get 1 }}
```

​	当输出取决于参数是否设置时，使用`with` 很棒：

```go-html-template
{{ with .Get "class" }} class="{{ . }}"{{ end }}
```

​	`.Get` 也可以用于检查是否已提供参数。当条件取决于两个值中的任一个或两个值时，这非常有用：

```go-html-template
{{ if or (.Get "title") (.Get "alt") }} alt="{{ with .Get "alt" }}{{ . }}{{ else }}{{ .Get "title" }}{{ end }}"{{ end }}
```

#### `.Inner` 

​	如果使用了闭合的简码，`.Inner` 变量将被填充为开放和闭合简码之间的内容。如果需要闭合的简码，则可以检查 `.Inner` 的长度以指示其存在。

​	通过`.Inner`变量声明内容的简码也可以使用自闭合语法来声明，而无需内容和结束标签：

```go-html-template
\{\{\< innershortcode \/\>\}\}
```

> 任何引用`.Inner`的简码都必须是闭合的或自闭合的。

#### `.Params` 

​	简码中的`.Params`变量包含传递给简码的参数列表，用于更复杂的用例。您也可以使用以下逻辑访问更高级别的参数：

- `$.Params`

  这些是直接传递到简码声明中的参数（例如，YouTube视频ID）

- `$.Page.Params`

  引用该页面的参数；在这种情况下， 该"page"指的是声明简码的内容文件（例如，内容的前置元数据中的`shortcode_color`字段可以通过`$.Page.Params.shortcode_color`访问）。

- `$.Page.Site.Params`

  引用您[站点配置文件](https://gohugo.io/getting-started/configuration/)中定义的全局变量。
  
  

#### `.IsNamedParams` 

​	`.IsNamedParams` 变量检查简码声明是否使用了命名参数，并返回一个布尔值。

​	例如，您可以创建一个 `image` 简码，可以使用命名参数 `src` 或第一个位置参数，具体取决于内容作者的偏好。假设 `image` 简码的调用方式如下：

```go-html-template
\{\{\< image src="images/my-image.jpg" \>\}\}
```

​	然后，您可以将以下内容包含在您的简码模板中：

```go-html-template
{{ if .IsNamedParams }}
<img src="{{ .Get "src" }}" alt="">
{{ else }}
<img src="{{ .Get 0 }}" alt="">
{{ end }}
```

​	请查看下面的 [Vimeo 简码示例](https://gohugo.io/templates/shortcode-templates/#single-flexible-example-vimeo) 以了解 `.IsNamedParams` 的用法。

​	虽然可以创建接受位置参数和命名参数的简码模板，但是在内容中声明的简码不能混合参数类型。因此，像 `\{\{\< image src="images/my-image.jpg" "This is my alt text" \>\}\}` 这样声明的简码将返回一个错误。

​	您还可以使用变量`.Page`访问所有普通[页面变量](https://gohugo.io/variables/page/)。

​	简码也可以嵌套。在嵌套的简码标签中，您可以使用 [`.Parent` 变量](https://gohugo.io/variables/shortcodes/) 访问父级简码的上下文，这对于从根继承常见的简码参数非常有用。

### 检查是否存在 

​	您可以通过在该页面模板中调用`.HasShortcode`，并提供简码的名称来检查页面上是否使用了特定的简码。当您想要在头部中包含仅由该简码使用的特定脚本或样式时，这一功能有时很有用。

## 自定义简码示例 

​	以下是通过在`/layouts/shortcodes`中的简码模板文件创建的不同类型的简码示例。

### 单词示例：`year` 

​	假设您想在不需要不断查看 Markdown 的情况下，在内容文件中保持版权年份的更新。您的目标是可以按照以下方式调用简码：

```go-html-template
\{\{\< year \>\}\}
```

/layouts/shortcodes/year.html

```go-html-template
{{ now.Format "2006" }}
```

### 单位置示例：`YouTube` 

​	内嵌视频是 Markdown 内容中常见的补充，但很容易变得不美观。以下是 [Hugo 的内置 YouTube 简码](https://gohugo.io/content-management/shortcodes/#youtube) 使用的代码：

```go-html-template
\{\{\< youtube 09jf3ow9jfw \>\}\}
```

​	将会加载 `/layouts/shortcodes/youtube.html` 中的模板：

/layouts/shortcodes/youtube.html

```go-html-template
<div class="embed video-player">
<iframe class="youtube-player" type="text/html" width="640" height="385" src="https://www.youtube.com/embed/{{ index .Params 0 }}" allowfullscreen frameborder="0">
</iframe>
</div>
```

youtube-embed.html

```go-html-template
<div class="embed video-player">
    <iframe class="youtube-player" type="text/html"
        width="640" height="385"
        src="https://www.youtube.com/embed/09jf3ow9jfw"
        allowfullscreen frameborder="0">
    </iframe>
</div>
```

### 单命名示例：`image` 

​	假设您想创建自己的 `img` 简码，而不是使用 Hugo 的内置 [`figure` 简码](https://gohugo.io/content-management/shortcodes/#figure)。您的目标是可以在内容文件中按照以下方式调用简码：

content-image.md

```md
\{\{\< img src="/media/spf13.jpg" title="Steve Francia" \>\}\}
```

​	您已经在 `/layouts/shortcodes/img.html` 中创建了简码，它会加载以下简码模板：

/layouts/shortcodes/img.html

```go-html-template
<!-- image -->
<figure {{ with .Get "class" }}class="{{ . }}"{{ end }}>
  {{ with .Get "link" }}<a href="{{ . }}">{{ end }}
    <img src="{{ .Get "src" }}" {{ if or (.Get "alt") (.Get "caption") }}alt="{{ with .Get "alt" }}{{ . }}{{ else }}{{ .Get "caption" }}{{ end }}"{{ end }} />
    {{ if .Get "link" }}</a>{{ end }}
    {{ if or (or (.Get "title") (.Get "caption")) (.Get "attr") }}
      <figcaption>{{ if isset .Params "title" }}
        <h4>{{ .Get "title" }}</h4>{{ end }}
        {{ if or (.Get "caption") (.Get "attr") }}<p>
        {{ .Get "caption" }}
        {{ with .Get "attrlink" }}<a href="{{ . }}"> {{ end }}
          {{ .Get "attr" }}
        {{ if .Get "attrlink" }}</a> {{ end }}
        </p> {{ end }}
      </figcaption>
  {{ end }}
</figure>
<!-- image -->
```

​	将被渲染为：

img-output.html

```go-html-template
<figure>
  <img src="/media/spf13.jpg"  />
  <figcaption>
      <h4>Steve Francia</h4>
  </figcaption>
</figure>
```

### 单灵活示例：`vimeo`

```go-html-template
\{\{\< vimeo 49718712 \>\}\}
\{\{\< vimeo id="49718712" class="flex-video" \>\}\}
```

​	将会加载 `/layouts/shortcodes/vimeo.html` 中的模板：

/layouts/shortcodes/vimeo.html

```go-html-template
{{ if .IsNamedParams }}
  <div class="{{ if .Get "class" }}{{ .Get "class" }}{{ else }}vimeo-container{{ end }}">
    <iframe src="https://player.vimeo.com/video/{{ .Get "id" }}" allowfullscreen></iframe>
  </div>
{{ else }}
  <div class="{{ if len .Params | eq 2 }}{{ .Get 1 }}{{ else }}vimeo-container{{ end }}">
    <iframe src="https://player.vimeo.com/video/{{ .Get 0 }}" allowfullscreen></iframe>
  </div>
{{ end }}
```

​	将被渲染为：

vimeo-iframes.html

```go-html-template
<div class="vimeo-container">
  <iframe src="https://player.vimeo.com/video/49718712" allowfullscreen></iframe>
</div>
<div class="flex-video">
  <iframe src="https://player.vimeo.com/video/49718712" allowfullscreen></iframe>
</div>
```

### 成对示例：`highlight` 

​	以下内容取自 `highlight`，它是 Hugo [内置简码](https://gohugo.io/content-management/shortcodes/) 之一。

highlight-example.md

```md
\{\{\< highlight html \>\}\}
  <html>
    <body> This HTML </body>
  </html>
\{\{\< /highlight \>\}\}
```

​	`highlight` 简码的模板使用以下代码，它已经包含在 Hugo 中：

```go-html-template
{{ .Get 0 | highlight .Inner }}
```

​	HTML 示例代码块的渲染输出如下：

syntax-highlighted.html

```go-html-template
<div class="highlight" style="background: #272822"><pre style="line-height: 125%"><span style="color: #f92672">&lt;html&gt;</span>
    <span style="color: #f92672">&lt;body&gt;</span> This HTML <span style="color: #f92672">&lt;/body&gt;</span>
<span style="color: #f92672">&lt;/html&gt;</span>
</pre></div>
```

### 嵌套的简码：图像库 

​	Hugo的[`.Parent` 简码变量](https://gohugo.io/variables/shortcodes/)在*父*简码的上下文中被调用时提供了对父简码上下文的访问，这为常见的简码参数提供了继承模型。

​	下面的示例是人为的，但演示了该概念。假设您有一个 `gallery` 简码，它期望一个名为 `class` 的参数：

layouts/shortcodes/gallery.html

```go-html-template
<div class="{{ .Get "class" }}">
  {{ .Inner }}
</div>
```

​	您还有一个 `img` 简码，只有一个名为 `src` 的参数，您想在 `gallery` 和其他简码中调用它，以使父级定义每个 `img` 的上下文：

layouts/shortcodes/img.html

```go-html-template
{{- $src := .Get "src" -}}
{{- with .Parent -}}
  <img src="{{ $src }}" class="{{ .Get "class" }}-image">
{{- else -}}
  <img src="{{ $src }}">
{{- end -}}
```

​	然后您可以在内容中按以下方式调用您的简码：

```go-html-template
\{\{\< gallery class="content-gallery" \>\}\}
  \{\{\< img src="/images/one.jpg" \>\}\}
  \{\{\< img src="/images/two.jpg" \>\}\}
\{\{\< /gallery \>\}\}
\{\{\< img src="/images/three.jpg" \>\}\}
```

​	这将输出以下 HTML。请注意，前两个 `img` 简码继承了通过调用父级 `gallery` 设置的 `class` 值为 `content-gallery`，而第三个 `img` 只使用了 `src`：

```html
<div class="content-gallery">
    <img src="/images/one.jpg" class="content-gallery-image">
    <img src="/images/two.jpg" class="content-gallery-image">
</div>
<img src="/images/three.jpg">
```

## 简码中的错误处理 

​	使用 [errorf](https://gohugo.io/functions/errorf) 模板函数和 [.Position](https://gohugo.io/variables/shortcodes/) 变量可获得简码中有用的错误消息：

```bash
{{ with .Get "name" }}
{{ else }}
{{ errorf "missing value for param 'name': %s" .Position }}
{{ end }}
```

​	当上述失败时，您会看到类似下面的 `ERROR` 日志：

```bash
ERROR 2018/11/07 10:05:55 missing value for param name: "/Users/bep/dev/go/gohugoio/hugo/docs/content/en/variables/shortcodes.md:32:1"
```

## 更多简码示例 

​	更多简码示例可以在 [spf13.com 的简码目录](https://github.com/spf13/spf13.com/tree/master/layouts/shortcodes) 和 [Hugo 文档的简码目录](https://github.com/gohugoio/hugo/tree/master/docs/layouts/shortcodes) 中找到。

## 内联简码 

​	您也可以内联实现您的简码——例如，在您使用它们的内容文件中。这对于您只需要在一个地方使用脚本非常有用。

​	这个功能默认是禁用的，但可以在您的站点配置中启用：

config.

=== "yaml"

    ``` yaml
    enableInlineShortcodes: true
    ```

=== "toml"

    ``` toml
    enableInlineShortcodes = true
    ```

=== "json"

    ``` json
    {
       "enableInlineShortcodes": true
    }
    ```



​	它出于安全原因默认禁用。Hugo 模板处理使用的安全模型假定模板作者是可信的，但内容文件不是，因此模板是安全的，可以避免因输入数据格式不正确而出现注入问题。但在大多数情况下，您也可以完全控制内容，那么 `enableInlineShortcodes = true` 将被认为是安全的。但要注意：它允许从内容文件中执行 ad-hoc [Go 文本模板](https://golang.org/pkg/text/template/)。

​	启用后，您可以在内容文件中执行以下操作：

```go-text-template
\{\{\< time.inline \>\}\}{{ now }}\{\{\< /time.inline \>\}\}
```

​	上述代码将打印当前日期和时间。

请注意，内联简码的内部内容将被解析并作为一个具有与常规简码模板相同上下文的 Go 文本模板执行。

​	这意味着可以通过`.Page.Title`等方式访问当前页面。这也意味着没有"嵌套内联简码"的概念。

​	同一个内联简码可以在同一个内容文件中多次重复使用，如果需要不同的参数，则使用自闭合语法：

```go-text-template
\{\{\< time.inline /\>\}\}
```

## 另请参阅

- [简码 ](https://gohugo.io/content-management/shortcodes/)
- [.Get](https://gohugo.io/functions/get/)
- [Hugo的查找顺序 ](https://gohugo.io/templates/lookup-order/)
- [RSS模板 ](https://gohugo.io/templates/rss/)
- [章节页面模板](https://gohugo.io/templates/section-templates/)
