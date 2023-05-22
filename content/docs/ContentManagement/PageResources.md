+++
title = "页面资源"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Page Resources - 页面资源 

[https://gohugo.io/content-management/page-resources/](https://gohugo.io/content-management/page-resources/)

​	页面资源（如图片、其他页面、文档等）具有相对于页面的 URL 和它们自己的元数据。 

​	页面资源只能从[page bundles](https://gohugo.io/content-management/page-bundles)中访问，这些目录在其根目录中具有index.md或_index.md文件。页面资源仅可用于与其捆绑的页面。

​	在此示例中，`first-post`是具有10个页面资源（包括音频，数据，文档，图像和视频）访问权限的page bundle。尽管`second-post`也是一个page bundle，但它没有页面资源，并且无法直接访问与`first-post`关联的页面资源。

```text
content
└── post
    ├── first-post
    │   ├── images
    │   │   ├── a.jpg
    │   │   ├── b.jpg
    │   │   └── c.jpg
    │   ├── index.md (root of page bundle)
    │   ├── latest.html
    │   ├── manual.json
    │   ├── notice.md
    │   ├── office.mp3
    │   ├── pocket.mp4
    │   ├── rating.pdf
    │   └── safety.txt
    └── second-post
        └── index.md (root of page bundle)
```

## 属性

- ResourceType

  ​	该资源[媒体类型](https://gohugo.io/templates/output-formats/#media-types)的主类型。例如，MIME类型为`image/jpeg`的文件的`ResourceType`为`image`。页面的`ResourceType`值为`page`。 

- Name

  默认值为文件名（相对于所属页面）。可以在前置元数据中设置。 

- Title

  默认值与 `.Name` 相同。可以在前置元数据中设置。 

- Permalink

  该资源的绝对URL。类型为`page`的资源将没有值。 

- RelPermalink

  该资源的相对URL。类型为`page`的资源将没有值。 

- Content

  该资源本身的内容。对于大多数资源，这将返回一个字符串，其中包含文件的内容。使用它来创建内联资源。

```go-html-template
{{ with .Resources.GetMatch "script.js" }}
  <script>{{ .Content | safeJS }}</script>
{{ end }}

{{ with .Resources.GetMatch "style.css" }}
  <style>{{ .Content | safeCSS }}</style>
{{ end }}

{{ with .Resources.GetMatch "img.png" }}
  <img src="data:{{ .MediaType }};base64,{{ .Content | base64Encode }}">
{{ end }}
```

- MediaType

  该资源的MIME类型，例如`image/jpeg`。 

- MediaType.MainType

  该资源MIME类型的主类型。例如，MIME类型为`application/pdf`的文件的主类型为`application`。 

- MediaType.SubType

  该资源MIME类型的子类型。例如，MIME类型为`application/pdf`的文件的子类型为`pdf`。请注意，这与文件扩展名不同 ——  PowerPoint文件的子类型为`vnd.mspowerpoint`。 

- MediaType.Suffixes

  该资源MIME类型的可能后缀切片。

## 方法

- ByType

  返回给定类型的页面资源。 

```go-html-template
{{ .Resources.ByType "image" }}
```

- Match

  返回所有`Name`与给定通配符模式（[examples](https://github.com/gobwas/glob/blob/master/readme.md)）匹配的页面资源（作为切片）。匹配不区分大小写。 

```go-html-template
{{ .Resources.Match "images/*" }}
```

- GetMatch

  与`Match`相同，但将返回第一个匹配项。

### 模式匹配

```go
// 使用 Match/GetMatch 来寻找这个 images/sunset.jpg ?
.Resources.Match "images/sun*" ✅
.Resources.Match "**/sunset.jpg" ✅
.Resources.Match "images/*.jpg" ✅
.Resources.Match "**.jpg" ✅
.Resources.Match "*" 🚫
.Resources.Match "sunset.jpg" 🚫
.Resources.Match "*sunset.jpg" 🚫
```

## 页面资源元数据 

​	页面资源的元数据由相应页面的前置元数据中的`resources`数组/表（array/table）参数进行管理。您可以使用[通配符](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm)进行批量分配值。

> ​	类型为`page`的资源从其自己的前置元数据中获取`Title`等。
>

- name

  设置`Name`中返回的值

> ​	`Match`，`Get`和`GetMatch`方法使用`Name`来匹配资源。
>

- title

  设置`Title`中返回的值。 

- params

  一个自定义键/值的映射。 

### 资源元数据示例

=== "yaml"

    ``` yaml
    date: "2018-01-25"
    resources:
    - name: header
      src: images/sunset.jpg
    - params:
        icon: photo
      src: documents/photo_specs.pdf
      title: Photo Specifications
    - src: documents/guide.pdf
      title: Instruction Guide
    - src: documents/checklist.pdf
      title: Document Checklist
    - src: documents/payment.docx
      title: Proof of Payment
    - name: pdf-file-:counter
      params:
        icon: pdf
      src: '**.pdf'
    - params:
        icon: word
      src: '**.docx'
    title: Application
    ```

=== "toml"

    ``` toml
    date = '2018-01-25'
    title = 'Application'
    [[resources]]
    name = 'header'
    src = 'images/sunset.jpg'
    [[resources]]
    src = 'documents/photo_specs.pdf'
    title = 'Photo Specifications'
    [resources.params]
      icon = 'photo'
    [[resources]]
    src = 'documents/guide.pdf'
    title = 'Instruction Guide'
    [[resources]]
    src = 'documents/checklist.pdf'
    title = 'Document Checklist'
    [[resources]]
    src = 'documents/payment.docx'
    title = 'Proof of Payment'
    [[resources]]
    name = 'pdf-file-:counter'
    src = '**.pdf'
    [resources.params]
      icon = 'pdf'
    [[resources]]
    src = '**.docx'
    [resources.params]
      icon = 'word'
    ```

=== "json"

    ``` json
    {
       "date": "2018-01-25",
       "resources": [
          {
             "name": "header",
             "src": "images/sunset.jpg"
          },
          {
             "params": {
                "icon": "photo"
             },
             "src": "documents/photo_specs.pdf",
             "title": "Photo Specifications"
          },
          {
             "src": "documents/guide.pdf",
             "title": "Instruction Guide"
          },
          {
             "src": "documents/checklist.pdf",
             "title": "Document Checklist"
          },
          {
             "src": "documents/payment.docx",
             "title": "Proof of Payment"
          },
          {
             "name": "pdf-file-:counter",
             "params": {
                "icon": "pdf"
             },
             "src": "**.pdf"
          },
          {
             "params": {
                "icon": "word"
             },
             "src": "**.docx"
          }
       ],
       "title": "Application"
    }
    ```

从上面的示例中：

- `sunset.jpg`将获得一个新的`Name`，并且现在可以使用`.GetMatch "header"`找到它。 
- `documents/photo_specs.pdf`将获得`photo`图标。 
- `documents/checklist.pdf`，`documents/guide.pdf`和`documents/payment.docx`将得到`Title`，如`Title`中所设置。 
- 包中除`documents/photo_specs.pdf`外的每个PDF都将获得`pdf`图标。 
- 所有`PDF`文件都将获得新的`Name`。`name`参数包含一个特殊占位符`:counter`，因此名称将是`pdf-file-1`、`pdf-file-2`、`pdf-file-3`。 
- 包中的每个docx都将获得`word`图标。 

​	顺序很重要 —— 只有`title`，`name`和`params`-keys的第一个设置值将被使用。连续的参数仅设置未设置的参数。在上面的示例中，`.Params.icon`首先在`src = "documents/photo_specs.pdf"`中设置为`"photo"`。因此，后来设置的`src = "**.pdf"`规则不会将其覆盖为`"pdf"`。

### `name` 和 `title` 中的 `:counter` 占位符 



​	`:counter`是在资源的`name`和`title`参数中识别的特殊占位符。

​	该计数器从第一次在`name`或`title`中使用时开始计数。

​	例如，如果一个包中有资源`photo_specs.pdf`，`other_specs.pdf`，`guide.pdf`和`checklist.pdf`，并且前置元数据已将`resources`指定为：

=== "yaml"

    ``` yaml
    resources:
    - src: '*specs.pdf'
      title: 'Specification #:counter'
    - name: pdf-file-:counter
      src: '**.pdf'
    ```

=== "toml"

    ``` toml
    [[resources]]
    src = '*specs.pdf'
    title = 'Specification #:counter'
    [[resources]]
    name = 'pdf-file-:counter'
    src = '**.pdf'
    ```

=== "json"

    ``` json
    {
       "resources": [
          {
             "src": "*specs.pdf",
             "title": "Specification #:counter"
          },
          {
             "name": "pdf-file-:counter",
             "src": "**.pdf"
          }
       ]
    }
    ```

则`Name`和`Title`将按如下分配给资源文件：

| Resource file   | `Name`            | `Title`              |
| :-------------- | :---------------- | :------------------- |
| checklist.pdf   | `"pdf-file-1.pdf` | `"checklist.pdf"`    |
| guide.pdf       | `"pdf-file-2.pdf` | `"guide.pdf"`        |
| other_specs.pdf | `"pdf-file-3.pdf` | `"Specification #1"` |
| photo_specs.pdf | `"pdf-file-4.pdf` | `"Specification #2"` |

## 另请参阅 

- [内容组织 ](https://gohugo.io/content-management/organization/)
- [.Scratch](https://gohugo.io/functions/scratch/)
- [.Store](https://gohugo.io/functions/store/)
- [构建选项 ](https://gohugo.io/content-management/build-options/)
- [评论](https://gohugo.io/content-management/comments/)
