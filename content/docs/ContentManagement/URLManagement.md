+++
title = "URL管理"
weight = 16
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# URL Management - URL管理 

[https://gohugo.io/content-management/urls/](https://gohugo.io/content-management/urls/)

​	通过前置元数据输入和站点配置中的设置来控制URL的结构和外观。 

## 概述 

​	默认情况下，当Hugo渲染页面时，生成的URL与`content`目录中的文件路径匹配。例如：

```text
content/posts/post-1.md → https://example.org/posts/post-1/
```

​	您可以通过前置元数据值和站点配置选项来更改URL的结构和外观。

## 前置元数据 

### `slug` 

Set the `slug` in 前置元数据 to override the last segment of the path. The `slug` value does not affect section pages.

​	在前置元数据中设置`slug`以覆盖路径的最后一段。`slug`值不影响部分页面。

content/posts/post-1.md

=== "yaml"

    ``` yaml
    ---
    slug: my-first-post
    title: My First Post
    ---
    
    ```
=== "toml"

    ``` toml
    +++
    slug = 'my-first-post'
    title = 'My First Post'
    +++
    ```
=== "json"

    ``` json
    {
       "slug": "my-first-post",
       "title": "My First Post"
    }
    ```

​	结果的URL将是：

```text
https://example.org/posts/my-first-post/
```

### `url` 

​	在前置元数据中设置`url`以覆盖整个路径。将其用于常规页面或section页面。

​	具有以下前置元数据的：

content/posts/post-1.md

=== "yaml"

    ``` yaml
    ---
    title: My First Article
    url: /articles/my-first-article
    ---
    ```
=== "toml"

    ``` toml
    +++
    title = 'My First Article'
    url = '/articles/my-first-article'
    +++
    ```
=== "json"

    ``` json
    {
       "title": "My First Article",
       "url": "/articles/my-first-article"
    }
    ```

​	结果的URL将是：

```text
https://example.org/articles/my-first-article/
```

​	如果包括文件扩展名：

content/posts/post-1.md

=== "yaml"

    ``` yaml
    ---
    title: My First Article
    url: /articles/my-first-article.html
    ---
    ```
=== "toml"

    ``` toml
    +++
    title = 'My First Article'
    url = '/articles/my-first-article.html'
    +++
    ```
=== "json"

    ``` json
    {
       "title": "My First Article",
       "url": "/articles/my-first-article.html"
    }
    ```

结果的URL将是：

```text
https://example.org/articles/my-first-article.html
```

​	在单语站点中，带有或不带有前导斜杠的`url`值相对于`baseURL`。

​	在多语言站点中：

- 带有前导斜杠的`url`值相对于`baseURL`。 
- 没有前导斜杠的`url`值相对于`baseURL`加上语言前缀。

| Site type    | 前置元数据 `url` | Resulting URL                   |
| :----------- | :----------------- | :------------------------------ |
| monolingual  | `/about`           | `https://example.org/about/`    |
| monolingual  | `about`            | `https://example.org/about/`    |
| multilingual | `/about`           | `https://example.org/about/`    |
| multilingual | `about`            | `https://example.org/de/about/` |

​	如果在前置元数据中同时设置`slug`和`url`，则`url`值优先。

## 站点配置 

### Permalinks  永久链接 

​	在站点配置中，为顶层section内的常规页面设置URL模式。这是递归的，影响后代常规页面。

> ​	在站点配置中定义的`permalinks`不适用于section页面。要调整section页面的URL，请在前置元数据中设置`url`。
>

#### 例子 

​	使用此内容结构：

```text
content/
├── posts/
│   ├── _index.md
│   ├── post-1.md
│   └── post-2.md
└── _index.md
```

​	为`posts` section内的普通页面创建一个基于日期的递归层次结构：

config.

=== "yaml"

    ``` yaml
    posts: /posts/:year/:month/:title/
    ```
=== "toml"

    ``` toml
    posts = '/posts/:year/:month/:title/'
    ```
=== "json"

    ``` json
    {
       "posts": "/posts/:year/:month/:title/"
    }
    ```

​	发布站点的结构将是：

```text
public/
├── posts/
│   ├── 2023/
│   │   └── 03/
│   │       ├── post-1/
│   │       │   └── index.html
│   │       └── post-2/
│   │           └── index.html
│   └── index.html
├── favicon.ico
└── index.html
```

​	要为内容根目录中的常规页面创建基于日期的层次结构：

config.

=== "yaml"

    ``` yaml
    /: /:year/:month/:title/
    ```
=== "toml"

    ``` toml
    '/' = '/:year/:month/:title/'
    ```
=== "json"

    ``` json
    {
       "/": "/:year/:month/:title/"
    }
    ```

> ​	为内容根目录定义的URL模式不适用于递归。
>

​	使用相同的方法处理分类（taxonomies）。例如，要省略URL的分类段（taxonomy segment）：

config.

=== "yaml"

    ``` yaml
    tags: /:title/
    ```
=== "toml"

    ``` toml
    tags = '/:title/'
    ```
=== "json"

    ``` json
    {
       "tags": "/:title/"
    }
    ```

​	前置元数据`url`值优先于`permalinks`中定义的URL模式。

#### Tokens 

​	在定义URL模式时使用这些标记。前置元数据中的`date`字段确定与时间相关的标记的值。

- `:year`

  4位数字的年份 

- `:month`

  2位数字的月份 

- `:monthname`

  月份的名称 

- `:day`

  2位数字的日期 

- `:weekday`

  一周中的1位数字日期（星期日=0） 

- `:weekdayname`

  一周中日期的名称 

- `:yearday`

  1到3位数字的一年中的日期 

- `:section`

  内容的section 

- `:sections`

  内容的section层次结构。您可以使用切片语法选择section：`:sections[1:]` 包括除第一个部分以外的所有部分，`:sections[:last]` 包括除最后一个部分以外的所有部分，`:sections[last]` 仅包括最后一个部分，`:sections[1:2]` 包括第2个和第3个section (这里应该是由问题的：按照go的语法这里应该只包括第1个section才对吧)。请注意，这种切片访问不会抛出任何越界错误，因此您不必非常精确。 

- `:title`

  内容的标题 

- `:slug`

  内容的 slug（如果在前置元数据中未提供 slug，则使用title） 

- `:slugorfilename`

  内容的 slug（如果在前置元数据中未提供 slug，则使用文件名） 

- `:filename`

  内容的文件名（不包括扩展名） 

​	对于与时间有关的值，您还可以使用 Go 的 [time 包](https://pkg.go.dev/time#pkg-constants)中定义的布局字符串组件。例如：

config.

=== "yaml"

    ``` yaml
    permalinks:
      posts: /:06/:1/:2/:title/
    ```
=== "toml"

    ``` toml
    [permalinks]
      posts = '/:06/:1/:2/:title/'
    ```
=== "json"

    ``` json
    {
       "permalinks": {
          "posts": "/:06/:1/:2/:title/"
       }
    }
    ```



### 外观 

​	URL 的外观可以是丑陋的或漂亮的。

| Type   | Path             | URL                              |
| :----- | :--------------- | :------------------------------- |
| ugly   | content/about.md | `https://example.org/about.html` |
| pretty | content/about.md | `https://example.org/about/`     |

​	默认情况下，Hugo 生成漂亮的 URL。要生成丑陋的 URL，请更改您的站点配置：

config.

=== "yaml"

    ``` yaml
    uglyURLs: true
    ```
=== "toml"

    ``` toml
    uglyURLs = true
    ```
=== "json"

    ``` json
    {
       "uglyURLs": true
    }
    ```



### Post-processing 

​	Hugo 提供了两个相互排斥的配置选项，用于在渲染页面后更改 URL。

#### Canonical URLs （  规范化 URL ）

​	这是一个传统的配置选项，被模板函数和 markdown 渲染钩子取代，很可能会在[未来的版本中被删除](https://github.com/gohugoio/hugo/issues/4733)。

​	如果启用，Hugo 在渲染页面后执行搜索和替换。它搜索与 `action`、`href`、`src`、`srcset` 和 `url` 属性相关联的站点相对 URL（具有前导斜杠）。然后，它添加 `baseURL` 来创建绝对 URL。

```text
<a href="/about"> → <a href="https://example.org/about/">
<img src="/a.gif"> → <img src="https://example.org/a.gif">
```

​	这是一种不完美、蛮力的方法，会影响内容以及HTML属性。正如上面提到的，这是一个旧的配置选项，可能会在未来的版本中被删除。

启用方法如下：

config.

=== "yaml"

    ``` yaml
    canonifyURLs: true
    ```
=== "toml"

    ``` toml
    canonifyURLs = true
    ```
=== "json"

    ``` json
    {
       "canonifyURLs": true
    }
    ```



#### Relative URLs 

​	除非您创建的是可通过文件系统导航的无服务器站点，否则不要启用此选项。

​	如果启用此选项，Hugo将在渲染页面后执行搜索和替换。它将搜索与`action`、`href`、`src`、`srcset`和`url`属性相关的站点相对URL（带有前导斜杠）。然后将URL转换为相对于当前页面的URL。

​	例如，在渲染`content/posts/post-1`时：

```text
<a href="/about"> → <a href="../../about">
<img src="/a.gif"> → <img src="../../a.gif">
```

​	这是一种不完美、蛮力的方法，会影响内容以及HTML属性。正如上面提到的，除非您创建的是可通过文件系统导航的无服务器站点，否则不要启用此选项。

启用方法如下：

config.

=== "yaml"

    ``` yaml
    relativeURLs: true
    ```
=== "toml"

    ``` toml
    relativeURLs = true
    
    ```
=== "json"

    ``` json
    {
       "relativeURLs": true
    }
    
    ```



## 别名 

​	使用别名从旧URL重定向到新URL：

- 带有前导斜杠的别名相对于`baseURL`
- 没有前导斜杠的别名相对于当前目录 

### 示例

​	更改现有页面的文件名，并创建从先前URL到新URL的别名：

content/posts/new-file-name.md.

=== "yaml"

    ``` yaml
    aliases:
    - /posts/previous-file-name
    ```
=== "toml"

    ``` toml
    aliases = ['/posts/previous-file-name']
    
    ```
=== "json"

    ``` json
    {
       "aliases": [
          "/posts/previous-file-name"
       ]
    }
    
    ```



Each of these directory-relative aliases is equivalent to the site-relative alias above:

​	这些目录相对别名与上面的站点相对别名等效：

- `previous-file-name`

- `./previous-file-name`
- `../posts/previous-file-name`

​	您可以为当前页面创建多个别名：

content/posts/new-file-name.md.

=== "yaml"

    ``` yaml
    aliases:
    - previous-file-name
    - original-file-name
    ```
=== "toml"

    ``` toml
    aliases = ['previous-file-name', 'original-file-name']
    
    ```
=== "json"

    ``` json
    {
       "aliases": [
          "previous-file-name",
          "original-file-name"
       ]
    }
    
    ```



​	在多语言站点中，可以使用目录相对别名，或者使用站点相对别名包含语言前缀：

content/posts/new-file-name.de.md.

=== "yaml"

    ``` yaml
    aliases:
    - /de/posts/previous-file-name
    ```
=== "toml"

    ``` toml
    aliases = ['/de/posts/previous-file-name']
    
    ```
=== "json"

    ``` json
    {
       "aliases": [
          "/de/posts/previous-file-name"
       ]
    }
    ```



### 别名的工作原理 

​	使用上面的第一个示例，Hugo 生成了以下站点结构：

```text
public/
├── posts/
│   ├── new-file-name/
│   │   └── index.html
│   ├── previous-file-name/
│   │   └── index.html
│   └── index.html
└── index.html
```

​	从旧的 URL 到新 URL 的别名是客户端重定向：

posts/previous-file-name/index.html

```go-html-template
<!DOCTYPE html>
<html lang="en-us">
  <head>
    <title>https://example.org/posts/new-file-name/</title>
    <link rel="canonical" href="https://example.org/posts/new-file-name/">
    <meta name="robots" content="noindex">
    <meta charset="utf-8">
    <meta http-equiv="refresh" content="0; url=https://example.org/posts/new-file-name/">
  </head>
</html>
```

Collectively, the elements in the `head` section:

​	`head` 部分的元素总结如下：

- 告诉搜索引擎新的 URL 是规范的（canonical） 
- 告诉搜索引擎不要索引旧的 URL 
- 告诉浏览器重定向到新的 URL 

​	Hugo 在渲染页面之前渲染别名文件。带有先前文件名的新页面将覆盖别名，这是预期的。

### 自定义 

​	创建一个新的模板（`layouts/alias.html`）来自定义别名文件的内容。该模板接收以下上下文：

- `Permalink`

  被别名的页面链接

- `Page`

  被别名的页面的 Page 数据 

## 另请参阅 

- [内容组织 ](https://gohugo.io/content-management/organization/)
- [配置 Hugo ](https://gohugo.io/getting-started/configuration/)
- [链接和交叉引用 ](https://gohugo.io/content-management/cross-references/)
- [菜单模板 ](https://gohugo.io/templates/menu-templates/)
- [菜单](https://gohugo.io/content-management/menus/)
