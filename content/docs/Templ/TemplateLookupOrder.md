+++
title = "Hugo 的查找顺序"
weight = 2
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Hugo's Lookup Order - Hugo 的查找顺序 

[https://gohugo.io/templates/lookup-order/](https://gohugo.io/templates/lookup-order/)

​	Hugo按照一定的顺序查找给定页面的布局，从最具体的布局开始。 

## Hugo 布局查找规则 

​	Hugo在选择给定页面的布局时会考虑下面列出的参数。它们按优先级排序。这应该很自然，但具体的参数变化请参考下面的表格。

- Kind

  页面的`Kind`（主页是其中之一）。请参见下面每个种类的示例表格。这也确定了它是单页面（即常规内容页面。然后我们在`_default/single.html`中寻找HTML模板）还是列表页面（章节列表、主页、分类列表、分类术语。然后我们在`_default/list.html`中寻找HTML模板）。 

- Layout

  可以在页面前置元数据中设置。 

- 输出格式 

  请参见[自定义输出格式](https://gohugo.io/templates/output-formats)。输出格式既有一个`name`（例如`rss`、`amp`、`html`），也有一个`suffix`（例如`xml`、`html`）。我们更喜欢两者匹配（例如`index.amp.html`），但寻找较不具体的模板。 

请注意，如果输出格式的媒体类型定义了多个后缀，则只考虑第一个后缀。

- Language

  模板名称中会考虑语言代码。如果站点语言是`fr`，则`index.fr.amp.html`将优于`index.amp.html`，但 `index.amp.html` 将在 `index.fr.html` 之前被选择。

- Type

  如果在前置元数据中设置了`type`的值，则它是`type`的值，否则它是根章节的名称（例如"blog"）。它总是有一个值，所以如果未设置，则值为"page"。 

- Section

  对于`section`、`taxonomy`和`term`类型很重要。 

> 提示：下面的示例看起来很长、很复杂。这就是灵活性在起作用。大多数Hugo站点只包含少量模板：
>
> ```bash
> ├── _default
> │   ├── baseof.html
> │   ├── list.html
> │   └── single.html
> └── index.html
> ```



## 带有主题的 Hugo 布局查找规则 

​	在Hugo中，布局可以存在于项目或主题的布局文件夹中，并且会选择最具体的布局。Hugo将交错查找下面的布局，找到最具体的一个布局，无论是在项目还是主题中。

## 指定一个模板

你不能改变查找内容页面的顺序，但是你可以改为让一个内容页面去指定一个模板。在前置类型元数据中指定类型、布局或者两者。

考虑这个内容结构：

```bash
content/
├── about.md
└── contact.md
```

在内容目录的根中文件有一个`page`的[内容类型](https://gohugo.io/getting-started/glossary/#content-type)。创建一个匹配的子目录，可以用单独一个模型去渲染这些页面：

```bash
layouts/
└── page/
    └── single.html
```

但是`contact`页面可能有一个表格和要求一个不同的模板。在前置类型元数据指定布局：

content/contact.md.
 
=== "yaml"

    ``` yaml
    layout: contact
    title: Contact
    ```

=== "toml"

    ``` toml
    layout = 'contact'
    title = 'Contact'
    ```

=== "json"

    ``` json
    {
       "googleAnalytics": "G-MEASUREMENT_ID"
    }
    ```

然后为`contact`页面创建模板：

```bash
layouts/
└── page/
    └── contact.html  <-- renders contact.md
    └── single.html   <-- renders about.md
```

作为一个内容类型，单词`page`是不准确的。可能`miscellaneous`将是更好的。添加`type`到每个页面的前置类型元数据：

content/about.md.
   
=== "yaml"

    ``` yaml
    title: About
    type: miscellaneous
    ```

=== "toml"

    ``` toml
    title = 'About'
    type = 'miscellaneous'
    ```

=== "json"

    ```json
    {
      "title": "About",
      "type": "miscellaneous"
    }
    ```

content/contact.md.
   
=== "yaml"

    ``` yaml
    layout: contact
    title: Contact
    type: miscellaneous
    ```

=== "toml"

    ``` toml
    layout = 'contact'
    title = 'Contact'
    type = 'miscellaneous'
    ```

=== "json"

    ```json
    {
      "layout": "contact",
      "title": "Contact",
      "type": "miscellaneous"
    }
    ```

现在放置布局进入相应的目录：

```bash
layouts/
└── miscellaneous/
    └── contact.html  <-- renders contact.md
    └── single.html   <-- renders about.md
```

## 示例：常规页面的布局查找

| Example                                                      | OutputFormat | Suffix | Template Lookup Order                                        |
| :----------------------------------------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| Single page in "posts" section                               | HTML         | html   | layouts/posts/single.html.htmllayouts/posts/single.htmllayouts/_default/single.html.htmllayouts/_default/single.html |
| Base template for single page in "posts" section             | HTML         | html   | layouts/posts/single-baseof.html.htmllayouts/posts/baseof.html.htmllayouts/posts/single-baseof.htmllayouts/posts/baseof.htmllayouts/_default/single-baseof.html.htmllayouts/_default/baseof.html.htmllayouts/_default/single-baseof.htmllayouts/_default/baseof.html |
| Single page in "posts" section with layout set               | HTML         | html   | layouts/posts/demolayout.html.htmllayouts/posts/single.html.htmllayouts/posts/demolayout.htmllayouts/posts/single.htmllayouts/_default/demolayout.html.htmllayouts/_default/single.html.htmllayouts/_default/demolayout.htmllayouts/_default/single.html |
| Base template for single page in "posts" section with layout set | HTML         | html   | layouts/posts/demolayout-baseof.html.htmllayouts/posts/single-baseof.html.htmllayouts/posts/baseof.html.htmllayouts/posts/demolayout-baseof.htmllayouts/posts/single-baseof.htmllayouts/posts/baseof.htmllayouts/_default/demolayout-baseof.html.htmllayouts/_default/single-baseof.html.htmllayouts/_default/baseof.html.htmllayouts/_default/demolayout-baseof.htmllayouts/_default/single-baseof.htmllayouts/_default/baseof.html |
| AMP single page                                              | AMP          | html   | layouts/posts/single.amp.htmllayouts/posts/single.htmllayouts/_default/single.amp.htmllayouts/_default/single.html |
| AMP single page, French language                             | AMP          | html   | layouts/posts/single.fr.amp.htmllayouts/posts/single.amp.htmllayouts/posts/single.fr.htmllayouts/posts/single.htmllayouts/_default/single.fr.amp.htmllayouts/_default/single.amp.htmllayouts/_default/single.fr.htmllayouts/_default/single.html |

## 示例：主页的布局查找

| Example                                   | OutputFormat | Suffix | Template Lookup Order                                        |
| :---------------------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| Home page                                 | HTML         | html   | layouts/index.html.htmllayouts/home.html.htmllayouts/list.html.htmllayouts/index.htmllayouts/home.htmllayouts/list.htmllayouts/_default/index.html.htmllayouts/_default/home.html.htmllayouts/_default/list.html.htmllayouts/_default/index.htmllayouts/_default/home.htmllayouts/_default/list.html |
| Base template for home page               | HTML         | html   | layouts/index-baseof.html.htmllayouts/home-baseof.html.htmllayouts/list-baseof.html.htmllayouts/baseof.html.htmllayouts/index-baseof.htmllayouts/home-baseof.htmllayouts/list-baseof.htmllayouts/baseof.htmllayouts/_default/index-baseof.html.htmllayouts/_default/home-baseof.html.htmllayouts/_default/list-baseof.html.htmllayouts/_default/baseof.html.htmllayouts/_default/index-baseof.htmllayouts/_default/home-baseof.htmllayouts/_default/list-baseof.htmllayouts/_default/baseof.html |
| Home page with type set                   | HTML         | html   | layouts/demotype/index.html.htmllayouts/demotype/home.html.htmllayouts/demotype/list.html.htmllayouts/demotype/index.htmllayouts/demotype/home.htmllayouts/demotype/list.htmllayouts/index.html.htmllayouts/home.html.htmllayouts/list.html.htmllayouts/index.htmllayouts/home.htmllayouts/list.htmllayouts/_default/index.html.htmllayouts/_default/home.html.htmllayouts/_default/list.html.htmllayouts/_default/index.htmllayouts/_default/home.htmllayouts/_default/list.html |
| Base template for home page with type set | HTML         | html   | layouts/demotype/index-baseof.html.htmllayouts/demotype/home-baseof.html.htmllayouts/demotype/list-baseof.html.htmllayouts/demotype/baseof.html.htmllayouts/demotype/index-baseof.htmllayouts/demotype/home-baseof.htmllayouts/demotype/list-baseof.htmllayouts/demotype/baseof.htmllayouts/index-baseof.html.htmllayouts/home-baseof.html.htmllayouts/list-baseof.html.htmllayouts/baseof.html.htmllayouts/index-baseof.htmllayouts/home-baseof.htmllayouts/list-baseof.htmllayouts/baseof.htmllayouts/_default/index-baseof.html.htmllayouts/_default/home-baseof.html.htmllayouts/_default/list-baseof.html.htmllayouts/_default/baseof.html.htmllayouts/_default/index-baseof.htmllayouts/_default/home-baseof.htmllayouts/_default/list-baseof.htmllayouts/_default/baseof.html |
| Home page with layout set                 | HTML         | html   | layouts/demolayout.html.htmllayouts/index.html.htmllayouts/home.html.htmllayouts/list.html.htmllayouts/demolayout.htmllayouts/index.htmllayouts/home.htmllayouts/list.htmllayouts/_default/demolayout.html.htmllayouts/_default/index.html.htmllayouts/_default/home.html.htmllayouts/_default/list.html.htmllayouts/_default/demolayout.htmllayouts/_default/index.htmllayouts/_default/home.htmllayouts/_default/list.html |
| AMP home, French language                 | AMP          | html   | layouts/index.fr.amp.htmllayouts/home.fr.amp.htmllayouts/list.fr.amp.htmllayouts/index.amp.htmllayouts/home.amp.htmllayouts/list.amp.htmllayouts/index.fr.htmllayouts/home.fr.htmllayouts/list.fr.htmllayouts/index.htmllayouts/home.htmllayouts/list.htmllayouts/_default/index.fr.amp.htmllayouts/_default/home.fr.amp.htmllayouts/_default/list.fr.amp.htmllayouts/_default/index.amp.htmllayouts/_default/home.amp.htmllayouts/_default/list.amp.htmllayouts/_default/index.fr.htmllayouts/_default/home.fr.htmllayouts/_default/list.fr.htmllayouts/_default/index.htmllayouts/_default/home.htmllayouts/_default/list.html |
| JSON home                                 | JSON         | json   | layouts/index.json.jsonlayouts/home.json.jsonlayouts/list.json.jsonlayouts/index.jsonlayouts/home.jsonlayouts/list.jsonlayouts/_default/index.json.jsonlayouts/_default/home.json.jsonlayouts/_default/list.json.jsonlayouts/_default/index.jsonlayouts/_default/home.jsonlayouts/_default/list.json |
| RSS home                                  | RSS          | xml    | layouts/index.rss.xmllayouts/home.rss.xmllayouts/rss.xmllayouts/list.rss.xmllayouts/index.xmllayouts/home.xmllayouts/list.xmllayouts/_default/index.rss.xmllayouts/_default/home.rss.xmllayouts/_default/rss.xmllayouts/_default/list.rss.xmllayouts/_default/index.xmllayouts/_default/home.xmllayouts/_default/list.xmllayouts/_internal/_default/rss.xml |

## 示例：章节页面的布局查找

| Example                                                      | OutputFormat | Suffix | Template Lookup Order                                        |
| :----------------------------------------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| RSS section posts                                            | RSS          | xml    | layouts/posts/section.rss.xmllayouts/posts/rss.xmllayouts/posts/list.rss.xmllayouts/posts/section.xmllayouts/posts/list.xmllayouts/section/section.rss.xmllayouts/section/rss.xmllayouts/section/list.rss.xmllayouts/section/section.xmllayouts/section/list.xmllayouts/_default/section.rss.xmllayouts/_default/rss.xmllayouts/_default/list.rss.xmllayouts/_default/section.xmllayouts/_default/list.xmllayouts/_internal/_default/rss.xml |
| Section list for "posts" section                             | HTML         | html   | layouts/posts/posts.html.htmllayouts/posts/section.html.htmllayouts/posts/list.html.htmllayouts/posts/posts.htmllayouts/posts/section.htmllayouts/posts/list.htmllayouts/section/posts.html.htmllayouts/section/section.html.htmllayouts/section/list.html.htmllayouts/section/posts.htmllayouts/section/section.htmllayouts/section/list.htmllayouts/_default/posts.html.htmllayouts/_default/section.html.htmllayouts/_default/list.html.htmllayouts/_default/posts.htmllayouts/_default/section.htmllayouts/_default/list.html |
| Section list for "posts" section with type set to "blog"     | HTML         | html   | layouts/blog/posts.html.htmllayouts/blog/section.html.htmllayouts/blog/list.html.htmllayouts/blog/posts.htmllayouts/blog/section.htmllayouts/blog/list.htmllayouts/posts/posts.html.htmllayouts/posts/section.html.htmllayouts/posts/list.html.htmllayouts/posts/posts.htmllayouts/posts/section.htmllayouts/posts/list.htmllayouts/section/posts.html.htmllayouts/section/section.html.htmllayouts/section/list.html.htmllayouts/section/posts.htmllayouts/section/section.htmllayouts/section/list.htmllayouts/_default/posts.html.htmllayouts/_default/section.html.htmllayouts/_default/list.html.htmllayouts/_default/posts.htmllayouts/_default/section.htmllayouts/_default/list.html |
| Section list for "posts" section with layout set to "demoLayout" | HTML         | html   | layouts/posts/demolayout.html.htmllayouts/posts/posts.html.htmllayouts/posts/section.html.htmllayouts/posts/list.html.htmllayouts/posts/demolayout.htmllayouts/posts/posts.htmllayouts/posts/section.htmllayouts/posts/list.htmllayouts/section/demolayout.html.htmllayouts/section/posts.html.htmllayouts/section/section.html.htmllayouts/section/list.html.htmllayouts/section/demolayout.htmllayouts/section/posts.htmllayouts/section/section.htmllayouts/section/list.htmllayouts/_default/demolayout.html.htmllayouts/_default/posts.html.htmllayouts/_default/section.html.htmllayouts/_default/list.html.htmllayouts/_default/demolayout.htmllayouts/_default/posts.htmllayouts/_default/section.htmllayouts/_default/list.html |

## 示例：分类页面的布局查找

| Example                     | OutputFormat | Suffix | Template Lookup Order                                        |
| :-------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| Taxonomy in categories      | RSS          | xml    | layouts/categories/category.terms.rss.xmllayouts/categories/terms.rss.xmllayouts/categories/taxonomy.rss.xmllayouts/categories/rss.xmllayouts/categories/list.rss.xmllayouts/categories/category.terms.xmllayouts/categories/terms.xmllayouts/categories/taxonomy.xmllayouts/categories/list.xmllayouts/category/category.terms.rss.xmllayouts/category/terms.rss.xmllayouts/category/taxonomy.rss.xmllayouts/category/rss.xmllayouts/category/list.rss.xmllayouts/category/category.terms.xmllayouts/category/terms.xmllayouts/category/taxonomy.xmllayouts/category/list.xmllayouts/taxonomy/category.terms.rss.xmllayouts/taxonomy/terms.rss.xmllayouts/taxonomy/taxonomy.rss.xmllayouts/taxonomy/rss.xmllayouts/taxonomy/list.rss.xmllayouts/taxonomy/category.terms.xmllayouts/taxonomy/terms.xmllayouts/taxonomy/taxonomy.xmllayouts/taxonomy/list.xmllayouts/_default/category.terms.rss.xmllayouts/_default/terms.rss.xmllayouts/_default/taxonomy.rss.xmllayouts/_default/rss.xmllayouts/_default/list.rss.xmllayouts/_default/category.terms.xmllayouts/_default/terms.xmllayouts/_default/taxonomy.xmllayouts/_default/list.xmllayouts/_internal/_default/rss.xml |
| Taxonomy list in categories | HTML         | html   | layouts/categories/category.terms.html.htmllayouts/categories/terms.html.htmllayouts/categories/taxonomy.html.htmllayouts/categories/list.html.htmllayouts/categories/category.terms.htmllayouts/categories/terms.htmllayouts/categories/taxonomy.htmllayouts/categories/list.htmllayouts/category/category.terms.html.htmllayouts/category/terms.html.htmllayouts/category/taxonomy.html.htmllayouts/category/list.html.htmllayouts/category/category.terms.htmllayouts/category/terms.htmllayouts/category/taxonomy.htmllayouts/category/list.htmllayouts/taxonomy/category.terms.html.htmllayouts/taxonomy/terms.html.htmllayouts/taxonomy/taxonomy.html.htmllayouts/taxonomy/list.html.htmllayouts/taxonomy/category.terms.htmllayouts/taxonomy/terms.htmllayouts/taxonomy/taxonomy.htmllayouts/taxonomy/list.htmllayouts/_default/category.terms.html.htmllayouts/_default/terms.html.htmllayouts/_default/taxonomy.html.htmllayouts/_default/list.html.htmllayouts/_default/category.terms.htmllayouts/_default/terms.htmllayouts/_default/taxonomy.htmllayouts/_default/list.html |

## 示例：术语页面的布局查找

| Example                     | OutputFormat | Suffix | Template Lookup Order                                        |
| :-------------------------- | :----------- | :----- | :----------------------------------------------------------- |
| Term in categories          | RSS          | xml    | layouts/categories/term.rss.xmllayouts/categories/category.rss.xmllayouts/categories/taxonomy.rss.xmllayouts/categories/rss.xmllayouts/categories/list.rss.xmllayouts/categories/term.xmllayouts/categories/category.xmllayouts/categories/taxonomy.xmllayouts/categories/list.xmllayouts/term/term.rss.xmllayouts/term/category.rss.xmllayouts/term/taxonomy.rss.xmllayouts/term/rss.xmllayouts/term/list.rss.xmllayouts/term/term.xmllayouts/term/category.xmllayouts/term/taxonomy.xmllayouts/term/list.xmllayouts/taxonomy/term.rss.xmllayouts/taxonomy/category.rss.xmllayouts/taxonomy/taxonomy.rss.xmllayouts/taxonomy/rss.xmllayouts/taxonomy/list.rss.xmllayouts/taxonomy/term.xmllayouts/taxonomy/category.xmllayouts/taxonomy/taxonomy.xmllayouts/taxonomy/list.xmllayouts/category/term.rss.xmllayouts/category/category.rss.xmllayouts/category/taxonomy.rss.xmllayouts/category/rss.xmllayouts/category/list.rss.xmllayouts/category/term.xmllayouts/category/category.xmllayouts/category/taxonomy.xmllayouts/category/list.xmllayouts/_default/term.rss.xmllayouts/_default/category.rss.xmllayouts/_default/taxonomy.rss.xmllayouts/_default/rss.xmllayouts/_default/list.rss.xmllayouts/_default/term.xmllayouts/_default/category.xmllayouts/_default/taxonomy.xmllayouts/_default/list.xmllayouts/_internal/_default/rss.xml |
| Taxonomy term in categories | HTML         | html   | layouts/categories/term.html.htmllayouts/categories/category.html.htmllayouts/categories/taxonomy.html.htmllayouts/categories/list.html.htmllayouts/categories/term.htmllayouts/categories/category.htmllayouts/categories/taxonomy.htmllayouts/categories/list.htmllayouts/term/term.html.htmllayouts/term/category.html.htmllayouts/term/taxonomy.html.htmllayouts/term/list.html.htmllayouts/term/term.htmllayouts/term/category.htmllayouts/term/taxonomy.htmllayouts/term/list.htmllayouts/taxonomy/term.html.htmllayouts/taxonomy/category.html.htmllayouts/taxonomy/taxonomy.html.htmllayouts/taxonomy/list.html.htmllayouts/taxonomy/term.htmllayouts/taxonomy/category.htmllayouts/taxonomy/taxonomy.htmllayouts/taxonomy/list.htmllayouts/category/term.html.htmllayouts/category/category.html.htmllayouts/category/taxonomy.html.htmllayouts/category/list.html.htmllayouts/category/term.htmllayouts/category/category.htmllayouts/category/taxonomy.htmllayouts/category/list.htmllayouts/_default/term.html.htmllayouts/_default/category.html.htmllayouts/_default/taxonomy.html.htmllayouts/_default/list.html.htmllayouts/_default/term.htmllayouts/_default/category.htmllayouts/_default/taxonomy.htmllayouts/_default/list.html |

## 另请参阅 

- [创建自己的简码](https://gohugo.io/templates/shortcode-templates/)
- [RSS 模板 ](https://gohugo.io/templates/rss/)
- [章节页面模板 ](https://gohugo.io/templates/section-templates/)
- [单页面模板 ](https://gohugo.io/templates/single-page-templates/)
- [站点地图模板](https://gohugo.io/templates/sitemap-template/)
