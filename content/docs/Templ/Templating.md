+++
title = "Hugo模板入门介绍"
weight = 1
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Introduction to Hugo Templating - Hugo模板入门介绍  

https://gohugo.io/templates/introduction/

​	Hugo 使用 Go 的 `html/template` 和 `text/template` 库作为模板的基础。 

​	以下仅为 Go 模板的入门指南。若想深入了解 Go 模板，请查看官方 [Go 文档](https://golang.org/pkg/text/template/)。

​	Go 模板提供了一种极其简单的模板语言，坚信只有最基本的逻辑应该放在模板或视图层中。

## 基本语法 

​	Go 模板是 HTML 文件，并加入了[变量](https://gohugo.io/variables)和[函数](https://gohugo.io/functions)。Go 模板的变量和函数可以在 `{{ }}`中进行访问。

### 访问预定义变量 

​	预定义变量可以是当前作用域中已经存在的变量（如下面[变量章节](https://gohugo.io/templates/introduction/#variables)的`.Title`示例），也可以是自定义变量（如该章节中的`$address`示例）。

```go-html-template
{{ .Title }}
{{ $address }}
```

​	函数的参数使用空格分隔。通常的语法如下：

```go-html-template
{{ FUNCTION ARG1 ARG2 .. }}
```

​	下面的示例使用`1`和`2`作为`add`函数的输入：

```go-html-template
{{ add 1 2 }}
```

#### 通过点符号访问方法和字段 

​	访问在内容前置元数据中定义的 Page 参数中的 `bar`。

```go-html-template
{{ .Params.bar }}
```

#### 括号可以用来分组项 

```go-html-template
{{ if or (isset .Params "alt") (isset .Params "caption") }} Caption {{ end }}
```

#### 单个语句可以分成多行 

```go-html-template
{{ if or
  (isset .Params "alt")
  (isset .Params "caption")
}}
```

#### 原始字符串字面值可以包含换行符

```go-html-template
{{ $msg := `Line one.
Line two.` }}
```

## 变量 

​	每个Go模板都有一个数据对象。在Hugo中，每个模板都传递了一个`Page`。在下面的示例中，`.Title`是[`Page`变量](https://gohugo.io/variables/page)中可访问的元素之一。

​	由于Page是模板的默认作用域，因此可以通过点前缀(`.Title`)轻松访问当前作用域(`.` —— "the **dot**")中的`Title`元素：

```go-html-template
<title>{{ .Title }}</title>
```

​	值也可以存储在自定义变量中，并在之后被引用：

​	自定义变量需要以`$`为前缀。

```go-html-template
{{ $address := "123 Main St." }}
{{ $address }}
```

​	使用`=`运算符可以重新定义变量。下面的示例在主页上打印"Var is Hugo Home"，在其他所有页面上打印"Var is Hugo Page"：

```go-html-template
{{ $var := "Hugo Page" }}
{{ if .IsHome }}
    {{ $var = "Hugo Home" }}
{{ end }}
Var is {{ $var }}
```

## 函数

​	Go模板仅提供了一些基本函数，但还提供了一种机制，使应用程序能够扩展原始函数集。

​	[Hugo模板函数](https://gohugo.io/functions)提供了特定于构建站点的附加功能。通过使用函数名和由空格分隔的所需参数来调用函数。如果没有重新编译Hugo，则无法添加模板函数。

### 示例1：添加数字

```go-html-template
{{ add 1 2 }}
<!-- prints 3 -->
```

### 示例2：比较数字

```go-html-template
{{ lt 1 2 }}
<!-- prints true (i.e., since 1 is less than 2) -->
```

​	请注意，这两个示例都使用了Go模板的[math](https://gohugo.io/functions/math)函数。

​	在[Go模板文档](https://golang.org/pkg/text/template/#hdr-Functions)中，有比Hugo文档中列出的更多的布尔运算符。

## Includes 

​	在包含（Include）另一个模板时，您需要传递它需要访问的数据。

​	为了传递当前上下文，请记住包含一个尾随点。

​	模板位置始终从Hugo的`layouts/`目录开始。

### Partial 

​	`partial`函数用于使用语法`{{ partial "<PATH>/<PARTIAL>.<EXTENSION>" . }}`包含部分（partial）模板。

​	包含`layouts/partials/header.html`部分（partial）模板的示例：

```go-html-template
{{ partial "header.html" . }}
```

### 模板 

​	在早期版本的Hugo中，`template`函数用于包含部分（partial）模板。现在，它仅用于调用[内部模板](https://gohugo.io/templates/internal)。语法为`{{ template "_internal/<TEMPLATE>.<EXTENSION>" . }}`。

​	可以在[这里](https://github.com/gohugoio/hugo/tree/master/tpl/tplimpl/embedded/templates)找到可用的内部模板。

​	包含内部`opengraph.html`模板的示例：

```go-html-template
{{ template "_internal/opengraph.html" . }}
```

## 逻辑 

​	Go模板提供了最基本的迭代和条件逻辑。

### 迭代

​	Go模板大量使用`range`来迭代map、array或slice。以下是如何使用`range`的不同示例。

#### 示例1：使用上下文(`.`) 

```go-html-template
{{ range $array }}
    {{ . }} <!-- The . represents an element in $array -->
{{ end }}
```

#### 示例2：为数组元素的值声明变量名 

```go-html-template
{{ range $elem_val := $array }}
    {{ $elem_val }}
{{ end }}
```

#### 示例3：为数组元素的索引和值声明变量名 

​	对于数组或切片，第一个声明的变量将映射到每个元素的索引。

```go-html-template
{{ range $elem_index, $elem_val := $array }}
   {{ $elem_index }} -- {{ $elem_val }}
{{ end }}
```

#### 示例4：为map元素的键和值声明变量名

​	对于map，第一个声明的变量将映射到每个map元素的键。

```go-html-template
{{ range $elem_key, $elem_val := $map }}
   {{ $elem_key }} -- {{ $elem_val }}
{{ end }}
```

#### 示例5：针对空map、数组或切片的条件语句 

​	如果传递给`range`的map、数组或切片长度为零，则将执行else语句。

```go-html-template
{{ range $array }}
    {{ . }}
{{ else }}
    <!-- This is only evaluated if $array is empty -->
{{ end }}
```

### 条件语句 

​	`if`、`else`、`with`、`or`、`and`和`not`提供了处理Go模板中条件逻辑的框架。与`range`一样，`if`和`with`语句也是用`{{ end }}`关闭的。

​	Go 模板将以下值视为`false`：

- `false` (boolean)
- `0` (integer)
- 任何长度为零的数组、切片、映射或字符串 

#### 示例1：`with`

​	通常使用`with`编写"if something exists, do this"这样的语句。

​	`with`会在其作用域内重新绑定上下文(`.`)（就像在`range`中一样）。

​	如果变量不存在，或者如果它按上面所述计算为"false"，则它会跳过该块。

```go-html-template
{{ with .Params.title }}
    <h4>{{ . }}</h4>
{{ end }}
```

#### 示例2：`with`..`else` 

​	下面的代码片段如果设置了"description"前置元数据的值，则使用它，否则使用默认的`.Summary`[页面变量](https://gohugo.io/variables/page)：

```go-html-template
{{ with .Param "description" }}
    {{ . }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

​	参见[`.Param`函数](https://gohugo.io/functions/param)。

#### 示例3：`if` 

​	编写`with`的另一种替代（更冗长）方法是使用`if`。在这里，`.`不会重新绑定。

​	下面的示例是使用`if`重写的"示例1"：

```go-html-template
{{ if isset .Params "title" }}
    <h4>{{ index .Params "title" }}</h4>
{{ end }}
```

#### 示例4：`if`..`else` 

​	下面的示例是使用`if` .. `else`重写的"示例2"，并使用[`isset`函数](https://gohugo.io/functions/isset)+ `.Params`变量（不同于[`.Param`函数](https://gohugo.io/functions/param)）：

```go-html-template
{{ if (isset .Params "description") }}
    {{ index .Params "description" }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

#### 示例5： `if` .. `else if` .. `else` 

​	与`with`不同，`if`还可以包含`else if`子句。

```go-html-template
{{ if (isset .Params "description") }}
    {{ index .Params "description" }}
{{ else if (isset .Params "summary") }}
    {{ index .Params "summary" }}
{{ else }}
    {{ .Summary }}
{{ end }}
```

#### 示例6： `and` & `or` 

```go-html-template
{{ if (and (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr")) }}
```

## 管道 

​	Go模板最强大的组件之一是能够将操作一层层堆叠在一起。这是通过使用管道来完成的。从Unix管道借鉴而来，概念很简单：每个管道的输出都成为下一个管道的输入。

​	由于Go模板的语法非常简单，因此管道对于能够链接在一起的函数调用非常重要。管道的一个限制是它们只能处理单个值，该值成为下一个管道的最后一个参数。

​	一些简单的示例应该有助于帮助您了解如何使用管道。

### 示例1： `shuffle` 

​	以下两个示例在功能上是相同的：

```go-html-template
{{ shuffle (seq 1 5) }}
{{ (seq 1 5) | shuffle }}
```

### 示例2： `index` 

​	以下访问名为"disqus_url"的页面参数并转义HTML。此示例还使用内置于Go模板中的[index函数](https://gohugo.io/functions/index-function/)：

```go-html-template
{{ index .Params "disqus_url" | html }}
```

### 示例3： 带有`isset`的`or` 

```go-html-template
{{ if or (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr") }}
Stuff Here
{{ end }}
```

可以重写为

```go-html-template
{{ if isset .Params "caption" | or isset .Params "title" | or isset .Params "attr" }}
Stuff Here
{{ end }}
```

## 上下文（也称"点"） 

​	Go模板最容易被忽视的理解概念是，`{{ . }}`始终指向当前上下文。 

- 在您的模板的顶层，它将是可用的数据集。 
- 但是，在迭代中，它将具有循环中当前项的值；即`{{ . }}`将不再引用整个页面可用的数据。 

​	如果您需要从循环内部访问页面级别的数据（例如，在前置元数据中设置的页面参数），则可能需要执行以下操作之一：

### 1.定义一个独立于上下文的变量 

​	以下示例演示如何定义一个独立于上下文的变量。

tags-range-with-page-variable.html

```go-html-template
{{ $title := .Site.Title }}
<ul>
{{ range .Params.tags }}
    <li>
        <a href="/tags/{{ . | urlize }}">{{ . }}</a>
        - {{ $title }}
    </li>
{{ end }}
</ul>
```

请注意，一旦我们进入循环（即 `range`），`{{ . }}` 的值就已经改变了。我们在循环外面定义了一个变量（`{{ $title }}`），并为其分配了一个值，以便我们可以从循环内部访问该值。

 

### 2.使用`$.`访问全局上下文 

​	`$` 在模板中具有特殊意义。`$`默认情况下被设置为 `.`（"the dot"）的起始值。这是[Go text/template的文档功能](https://golang.org/pkg/text/template/#hdr-Variables)。这意味着您可以从任何地方访问全局上下文。下面是先前的代码块的等效示例，但现在使用 `$` 从全局上下文中获取 `.Site.Title`：

range-through-tags-w-global.html

```go-html-template
<ul>
{{ range .Params.tags }}
  <li>
    <a href="/tags/{{ . | urlize }}">{{ . }}</a>
            - {{ $.Site.Title }}
  </li>
{{ end }}
</ul>
```

​	如果有人恶意重新定义特殊字符（例如 `{{ $ := .Site }}`），`$` 的内置魔力将停止工作。不要这样做。当然，您可以在全局上下文中使用 `{{ $ := . }}` 来重置 `$` 的默认值以恢复其功能。

## 空格

​	Go 1.6可以通过在相应的 `{{`或`}}`分隔符旁边包含连字符（`-`）和空格来修剪Go标记的两侧的空格的功能。

​	例如，以下Go模板将在其HTML输出中包含换行符和水平制表符：

```go-html-template
<div>
  {{ .Title }}
</div>
```

它将输出：

```html
<div>
  Hello, World!
</div>
```

​	在以下示例中使用`-`将删除围绕`.Title`变量的额外空格并删除换行符： 

```go-html-template
<div>
  {{- .Title -}}
</div>
```

它将输出：

```html
<div>Hello, World!</div>
```

Go 语言认为以下字符是空白字符：

- 空格 
- 水平制表符 
- 回车符 
- 换行符

## 注释

​	为了使您的模板组织有序并在团队之间共享信息，您可能希望向您的模板添加注释。在Hugo中有两种方法可以做到这一点。

### Go模板注释 

​	Go模板支持`{{/*`和`*/}}`来打开和关闭注释块。该块内的任何内容都不会被渲染。

例如：

```go-html-template
Bonsoir, {{/* {{ add 0 + 2 }} */}}Eliott.
```

将渲染`Bonsoir, Eliott.`，而不关心注释块中的语法错误（`add 0 + 2`）。

### HTML 注释

​	您可以通过将 HTML 代码注释的字符串管道化到 `safeHTML` 中来添加 HTML 注释。

例如：

```go-html-template
{{ "<!-- This is an HTML comment -->" | safeHTML }}
```

​	如果您需要使用变量构造这样的HTML注释，只需将`printf`管道化到`safeHTML`。

例如：

```go-html-template
{{ printf "<!-- Our website is named: %s -->" .Site.Title | safeHTML }}
```

#### 包含 Go 模板的 HTML 注释

​	默认情况下，HTML注释会被删除，但其内容仍将被求值。这意味着尽管HTML注释永远不会将任何内容渲染到最终的HTML页面，但其中包含的代码可能会导致构建过程失败。

​	不要尝试使用HTML注释来注释掉Go模板代码。

```go-html-template
<!-- {{ $author := "Emma Goldman" }} was a great woman. -->
{{ $author }}
```

​	模板引擎将删除HTML注释中的内容，但如果其中存在Go模板代码，则将首先求值任何Go模板代码。因此，上面的示例将渲染成`Emma Goldman`，因为`$author`变量在HTML注释中得到求值。但是，如果HTML注释中的代码有错误，构建将会失败。

## Hugo参数 

​	Hugo 提供了通过[站点配置](https://gohugo.io/getting-started/configuration)（用于整个站点的值）或每个特定内容的元数据（即[前置元数据](https://gohugo.io/content-management/front-matter)）向模板层传递值的选项。您可以定义任何类型的任何值，并在模板中任意使用它们，只要这些值得到[前置元数据格式](https://gohugo.io/content-management/front-matter#front-matter-formats)支持。

## 使用内容（`page`）参数 

​	您可以在单个内容的[前置元数据](https://gohugo.io/content-management/front-matter)中提供变量以供模板使用。

​	Hugo 文档中使用了一个示例。大多数页面都受益于提供目录，但有时目录并不合适。我们在前置元数据中定义了一个 `notoc` 变量，当设置为 `true` 时，将防止目录呈现。

以下是示例前置元数据：

content/example.md

=== "yaml"

    ``` yaml
    ---
    notoc: true
    title: Example
    ---
    ```

=== "toml"

    ``` toml
    +++
    notoc = true
    title = 'Example'
    +++
    ```

=== "json"

    ``` json
    {
       "notoc": true,
       "title": "Example"
    }
    ```



​	以下是可以在 `toc.html` [局部模板](https://gohugo.io/templates/partials)中使用的对应代码示例：

layouts/partials/toc.html

```go-html-template
{{ if not .Params.notoc }}
<aside>
  <header>
    <a href="#{{ .Title | urlize }}">
    <h3>{{ .Title }}</h3>
    </a>
  </header>
  {{ .TableOfContents }}
</aside>
<a href="#" id="toc-toggle"></a>
{{ end }}
```

​	我们希望页面的默认行为是包含目录，除非另有指定。此模板检查此页面前置元数据中的 `notoc:` 字段是否为 `true`。



## 使用站点配置参数 

​	您可以在[站点配置](https://gohugo.io/getting-started/configuration)文件中任意定义任何数量的站点级参数。这些参数在您的模板中全局可用。

​	例如，您可以声明以下内容：

config.

=== "yaml"

    ``` yaml
    params:
      copyrighthtml: Copyright &#xA9; 2017 John Doe. All Rights Reserved.
      sidebarrecentlimit: 5
      twitteruser: spf13
    ```

=== "toml"

    ``` toml
    [params]
      copyrighthtml = 'Copyright &#xA9; 2017 John Doe. All Rights Reserved.'
      sidebarrecentlimit = 5
      twitteruser = 'spf13'
    ```

=== "json"

    ``` json
    {
       "params": {
          "copyrighthtml": "Copyright \u0026#xA9; 2017 John Doe. All Rights Reserved.",
          "sidebarrecentlimit": 5,
          "twitteruser": "spf13"
       }
    }
    ```



​	在页脚布局中，您可以声明仅在提供了 `copyrighthtml` 参数时才呈现的 `<footer>`。如果提供了该参数，则需要通过 [`safeHTML` 函数](https://gohugo.io/functions/safehtml/)声明该字符串可以安全使用，以便 HTML 实体不会被再次转义。这使您可以轻松地每年 1 月 1 日仅更新顶级配置文件，而无需在模板中查找。

```go-html-template
{{ if .Site.Params.copyrighthtml }}
    <footer>
        <div class="text-center">{{ .Site.Params.CopyrightHTML | safeHTML }}</div>
    </footer>
{{ end }}
```

​	一种替代写"`if`"并引用同一值的方法是使用`with`。`with`在其作用域内重新绑定上下文(`.`)，如果该变量不存在，则跳过块：

layouts/partials/twitter.html

```go-html-template
{{ with .Site.Params.twitteruser }}
    <div>
        <a href="https://twitter.com/{{ . }}" rel="author">
        <img src="/images/twitter.png" width="48" height="48" title="Twitter: {{ . }}" alt="Twitter"></a>
    </div>
{{ end }}
```

​	最后，您也可以将"魔术常量"从您的布局中拉出来。以下示例使用`first`函数，以及`.RelPermalink`页面变量和`.Site.Pages`站点变量。

```go-html-template
<nav>
  <h1>Recent Posts</h1>
  <ul>
  {{- range first .Site.Params.SidebarRecentLimit .Site.Pages -}}
      <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
  {{- end -}}
  </ul>
</nav>    
```

## 示例：显示未来事件 

​	假设有以下内容结构和前置元数据：

```txt
content/
└── events/
    ├── event-1.md
    ├── event-2.md
    └── event-3.md
```

content/events/event-1.md.

=== "yaml"

    ``` yaml
    date: 2021-12-06T10:37:16-08:00
    draft: false
    end_date: 2021-12-05T11:00:00-08:00
    start_date: 2021-12-05T09:00:00-08:00
    title: Event 1
    ```

=== "toml"

    ``` toml
    date = 2021-12-06T10:37:16-08:00
    draft = false
    end_date = 2021-12-05T11:00:00-08:00
    start_date = 2021-12-05T09:00:00-08:00
    title = 'Event 1'
    ```

=== "json"

    ``` json
    {
       "date": "2021-12-06T10:37:16-08:00",
       "draft": false,
       "end_date": "2021-12-05T11:00:00-08:00",
       "start_date": "2021-12-05T09:00:00-08:00",
       "title": "Event 1"
    }
    ```

​	这个[局部模板](https://gohugo.io/templates/partials)渲染未来的事件：

layouts/partials/future-events.html

```go-html-template
<h2>Future Events</h2>
<ul>
  {{ range where site.RegularPages "Type" "events" }}
    {{ if gt (.Params.start_date | time.AsTime) now }}
      {{ $startDate := .Params.start_date | time.Format ":date_medium" }}
      <li>
        <a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a> - {{ $startDate }}
      </li>
    {{ end }}
  {{ end }}
</ul>
```

​	如果将前置元数据限制为TOML格式，并省略日期字段周围的引号，则可以执行日期比较而无需强制转换。

layouts/partials/future-events.html

```go-html-template
<h2>Future Events</h2>
<ul>
  {{ range where (where site.RegularPages "Type" "events") "Params.start_date" "gt" now }}
    {{ $startDate := .Params.start_date | time.Format ":date_medium" }}
    <li>
      <a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a> - {{ $startDate }}
    </li>
  {{ end }}
</ul>
```

## 另请参阅  

- [文件变量 ](https://gohugo.io/variables/files/)
- [菜单变量](https://gohugo.io/variables/menus/)
