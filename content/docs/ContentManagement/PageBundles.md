+++
title = "页面Bundle"
weight = 2
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Page Bundles - 页面Bundle

[https://gohugo.io/content-management/page-bundles/](https://gohugo.io/content-management/page-bundles/)

​	使用页面 Bundle 进行内容组织 

​	页面 Bundle 是一种分组[页面资源](https://gohugo.io/content-management/page-resources/)的方式。

​	页面 Bundle 可以是以下之一：

- 叶子Bundle (叶子表示它没有子级) 
- 分支Bundle (home page，section，taxonomy terms，taxonomy list) 

|                           | 叶子 Bundle                                                  | 分支 Bundle                                                  |
| :------------------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 用法                      | 单个页面内容和附件的集合                                     | 用于section页面（home page，section，taxonomy terms，taxonomy list）的附件集合 |
| 索引文件名                | `index.md` [1](https://gohugo.io/content-management/page-bundles/#fn:1) | `_index.md` [1](https://gohugo.io/content-management/page-bundles/#fn:1) |
| 允许的资源                | 页面和非页面类型（如图像、PDF 等）                           | 仅允许非页面类型（如图像、PDF 等）                           |
| 资源可以存放在哪里？      | 在叶子 Bundle 目录中的任何目录级别。                         | 仅在分支 Bundle 目录的目录级别中，即包含 `_index.md` 的目录（[参考](https://discourse.gohugo.io/t/question-about-content-folder-structure/11822/4?u=kaushalmodi)）。 |
| 布局类型                  | `single`                                                     | `list`                                                       |
| 嵌套                      | 不允许在其下方嵌套更多的 Bundle                              | 允许在其下方嵌套叶子或分支 Bundle                            |
| 示例                      | `content/posts/my-post/index.md`                             | `content/posts/_index.md`                                    |
| 非索引页面文件中的内容... | 仅作为页面资源访问                                           | 仅作为常规页面访问                                           |

## 叶子Bundles

​	叶子 Bundle 是 `content/` 目录中任何层次结构中包含 `index.md` 文件的目录。

### 叶子 Bundle 组织示例： 

```text
content/
├── about
│   ├── index.md
├── posts
│   ├── my-post
│   │   ├── content1.md
│   │   ├── content2.md
│   │   ├── image1.jpg
│   │   ├── image2.png
│   │   └── index.md
│   └── my-other-post
│       └── index.md
│
└── another-section
    ├── ..
    └── not-a-leaf-bundle
        ├── ..
        └── another-leaf-bundle
            └── index.md
```

In the above example `content/` directory, there are four leaf bundles:

​	在上面的示例中，`content/` 目录中有四个叶子 Bundle：

- `about`

  这个叶子 Bundle 在根级别（直接在 `content` 目录下）并且只有 `index.md`。 

- `my-post`

  这个叶子 Bundle 有 `index.md`、另外两个内容 Markdown 文件和两个图像文件。

  image1, image2：这些图像是 `my-post` 的页面资源，仅在 `my-post/index.md` 资源中可用。

  content1, content2: These content files are page resources of `my-post` and only available in `my-post/index.md` resources. They will **not** be rendered as individual pages. 这些内容文件是 my-post 的页面资源，仅在 my-post/index.md 资源中可用。它们不会被渲染为单独的页面。

- `my-other-post`

  这个叶子 Bundle 只有 `index.md`。 

- `another-leaf-bundle`

  这个叶子 Bundle 被嵌套在几个目录下。此 Bundle 也只有 `index.md`。

> ​	创建叶子 Bundle 的层次深度不重要，只要它不在另一个叶子 Bundle 中即可。
>

### Headless Bundle

​	无头Bundle是一种配置为不在任何地方发布的Bundle：

- 它将没有永久链接（`Permalink`）和`public/`中的渲染HTML。 
- 它不会成为`.Site.RegularPages`等的一部分。 

​	但是，您可以通过`.Site.GetPage`获取它。以下是一个示例：

```go-html-template
{{ $headless := .Site.GetPage "/some-headless-bundle" }}
{{ $reusablePages := $headless.Resources.Match "author*" }}
<h2>Authors</h2>
{{ range $reusablePages }}
    <h3>{{ .Title }}</h3>
    {{ .Content }}
{{ end }}
```

​	在此示例中，我们假设`some-headless-bundle`是一个包含一个或多个页面资源的无头Bundle，其`.Name`与`"author*"`匹配。

​	上面示例的说明：

1. 获取`some-headless-bundle`页面"object"。 
2. 使用`.Resources.Match`收集此页面Bundle中与`"author*"`匹配的资源片段。 
3. 循环遍历嵌套页面的切片，并输出它们的`.Title`和`.Content`。 

------

​	通过在`index.md`的前置元数据中添加以下内容，可以将一个叶子Bundle变为无头Bundle：

content/headless/index.md

=== "yaml"

    ```yaml
    ---
    headless: true
    ---
    ```

=== "toml"

    ```toml
    +++
    headless = true
    +++
    ```

=== "json"

    ```json
    {
       "headless": true
    }
    ```



​	此类无头页面Bundle有许多用例：

- 共享媒体库 
- 可重复使用的页面内容"snippets（片段）" 

## 分支Bundle 

​	分支Bundle是位于`content/`目录中任何层次结构中的任何目录，其中至少包含一个`_index.md`文件。

​	这个`_index.md`也可以直接在`content/`目录下。

> ​	这里以`md`（markdown）仅作为示例。只要它是Hugo可识别的内容类型，您可以使用任何文件类型作为内容资源。
>

### 分支Bundle组织示例 

```text
content/
├── branch-bundle-1
│   ├── branch-content1.md
│   ├── branch-content2.md
│   ├── image1.jpg
│   ├── image2.png
│   └── _index.md
└── branch-bundle-2
    ├── _index.md
    └── a-leaf-bundle
        └── index.md
```

​	在上面的`content/`目录示例中，有两个分支Bundle（和一个叶子Bundle）：

- `branch-bundle-1`

  该分支Bundle有`_index.md`，另外两个内容Markdown文件和两个图像文件。 

- `branch-bundle-2`

  该分支Bundle有`_index.md`和一个嵌套的叶子Bundle。 

> ​	创建分支Bundle的层次深度不重要。
>

------

1. `.md`扩展名仅作为示例。扩展名可以是`.html`，`.json`或任何有效的MIME类型。 ↩︎ ↩︎

## 另请参阅

- [内容组织 ](https://gohugo.io/content-management/organization/)
- [页面资源 ](https://gohugo.io/content-management/page-resources/)
- [单页模板](https://gohugo.io/templates/single-page-templates/)
