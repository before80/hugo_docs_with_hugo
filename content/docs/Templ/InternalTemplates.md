+++
title = "内置模板"
weight = 25
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Internal Templates - 内置模板 

[https://gohugo.io/templates/internal/](https://gohugo.io/templates/internal/)

​	Hugo自带一组样板模板，覆盖了静态站点最常见的用例。

​	虽然以下内置模板类似于局部模板，但它们不遵循局部模板查找顺序。

## Google Analytics 

​	Hugo自带内置模板支持Google Analytics，包括[Google Analytics 4](https://support.google.com/analytics/answer/10089681) (GA4)和Universal Analytics。

**注意:** Universal Analytics已被弃用。有关详情，请参阅[Universal Analytics将被取消](https://support.google.com/analytics/answer/11583528)。

### Configure Google Analytics 

​	在配置文件中提供您的跟踪ID：

**Google Analytics 4 (gtag.js)**

config.

=== "yaml"

    ``` yaml
    googleAnalytics: G-MEASUREMENT_ID
    ```

=== "toml"

    ``` toml
    googleAnalytics = 'G-MEASUREMENT_ID'
    ```

=== "json"

    ``` json
    {
       "googleAnalytics": "G-MEASUREMENT_ID"
    }
    ```



**Google Universal Analytics (analytics.js)**

config.

=== "yaml"

    ``` yaml
    googleAnalytics: UA-PROPERTY_ID
    ```

=== "toml"

    ``` toml
    googleAnalytics = 'UA-PROPERTY_ID'
    ```

=== "json"

    ``` json
    {
       "googleAnalytics": "UA-PROPERTY_ID"
    }
    ```



### 使用Google Analytics模板 

​	然后，您可以包含Google Analytics内置模板：

```go-html-template
{{ template "_internal/google_analytics_async.html" . }}
```

**注意:** 异步模板不适用于Google Analytics 4。

```go-html-template
{{ template "_internal/google_analytics.html" . }}
```

​	如果您想创建自己的模板，可以使用 `{{ site.Config.Services.GoogleAnalytics.ID }}` 访问已配置的ID。

## Disqus 

​	Hugo还带有用于[Disqus评论](https://disqus.com/)的内置模板，这是一种流行的静态和动态站点评论系统。要有效地使用Disqus，您需要通过[注册免费服务](https://disqus.com/profile/signup/)来获得Disqus "shortname"。

### 配置Disqus 

​	要使用Hugo的Disqus模板，您首先需要设置一个配置值：

config.

=== "yaml"

    ``` yaml
    disqusShortname: your-disqus-shortname
    ```

=== "toml"

    ``` toml
    disqusShortname = 'your-disqus-shortname'
    ```

=== "json"

    ``` json
    {
       "disqusShortname": "your-disqus-shortname"
    }
    ```



​	您还可以选择在给定篇的内容的前置元数据中设置以下值：

- `disqus_identifier`
- `disqus_title`
- `disqus_url`

### 使用Disqus模板 

​	要添加Disqus，请在要显示评论的模板中包含以下行：

```go-html-template
{{ template "_internal/disqus.html" . }}
```

​	还有一个暴露在配置中的 `.Site.DisqusShortname` 变量。

### Disqus评论的条件加载 

​	用户已经注意到，在运行Hugo Web服务器（即通过`hugo server`）时启用Disqus评论会导致在关联的Disqus帐户上创建不必要的讨论。

​	您可以创建以下 `layouts/partials/disqus.html` ：

layouts/partials/disqus.html

```go-html-template
<div id="disqus_thread"></div>
<script type="text/javascript">

(function() {
    // Don't ever inject Disqus on localhost--it creates unwanted
    // discussions from 'localhost:1313' on your Disqus account...
    if (window.location.hostname == "localhost")
        return;

    var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
    var disqus_shortname = '{{ .Site.DisqusShortname }}';
    dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
<a href="https://disqus.com/" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
```

​	当您在本地主机上运行时，`if` 语句将跳过Disqus评论注入的初始化。

​	然后可以按以下方式渲染自定义Disqus局部模板：

```go-html-template
{{ partial "disqus.html" . }}
```

## Open Graph 

​	Hugo提供了一个内置模板用于[Open Graph协议](https://ogp.me/)，这是一种元数据，可使页面成为社交图中的丰富对象。此格式用于Facebook和其他一些站点。

### 配置Open Graph 

​	Hugo的Open Graph模板使用配置变量和个别页面的[front-matter](https://gohugo.io/content-management/front-matter/)的混合来配置。

config.

=== "yaml"

    ``` yaml
    params:
      description: Text about my cool site
      images:
      - site-feature-image.jpg
      title: My cool site
    taxonomies:
      series: series
    ```

=== "toml"

    ``` toml
    [params]
      description = 'Text about my cool site'
      images = ['site-feature-image.jpg']
      title = 'My cool site'
    [taxonomies]
      series = 'series'
    ```

=== "json"

    ``` json
    {
       "params": {
          "description": "Text about my cool site",
          "images": [
             "site-feature-image.jpg"
          ],
          "title": "My cool site"
       },
       "taxonomies": {
          "series": "series"
       }
    }
    ```



content/blog/my-post.

=== "yaml"

    ``` yaml
    audio: []
    date: "2006-01-02"
    description: Text about this post
    images:
    - post-cover.png
    series: []
    tags: []
    title: Post title
    videos: []
    ```

=== "toml"

    ``` toml
    audio = []
    date = '2006-01-02'
    description = 'Text about this post'
    images = ['post-cover.png']
    series = []
    tags = []
    title = 'Post title'
    videos = []
    ```

=== "json"

    ``` json
    {
       "audio": [],
       "date": "2006-01-02",
       "description": "Text about this post",
       "images": [
          "post-cover.png"
       ],
       "series": [],
       "tags": [],
       "title": "Post title",
       "videos": []
    }
    ```



​	Hugo使用页面标题和描述作为标题和描述元数据。从 `images` 数组中取前6个URL用于图像元数据。如果使用[页面 bundles](https://gohugo.io/content-management/page-bundles/)，并且 `images` 数组为空或未定义，则使用与 `*feature*` 或 `*cover*,*thumbnail*` 匹配的文件名的图像用于图像元数据。

​	还可以设置各种可选的元数据：

- 日期、发布日期和最后修改日期用于设置发布时间元数据（如果指定）。
- `audio` and `videos` are URL arrays like `images` for the audio and video metadata tags, respectively.
- `audio` 和 `video` 是与音频和视频元数据标签对应的（与 `images` 类似） URL 数组。 
- 该页面上前 6 个 `tags` 用于标签（tags）元数据。
- `series` 分类法用于将相关的 "see also"页面放入同一系列。

​	如果使用 YouTube，这将生成一个类似于 `<meta property="og:video" content="url">` 的 og:video 标签。在 YouTube 视频中使用 `https://youtu.be/<id>` 格式（例如：`https://youtu.be/qtIqKaDlqXo`）。

### 使用 Open Graph 模板 

​	要添加 Open Graph 元数据，请在模板的 `<head>` 标签之间包含以下行：

```go-html-template
{{ template "_internal/opengraph.html" . }}
```

## Twitter Cards 

​	一个内置的模板，用于为链接到您的站点的推文附加丰富的媒体的[Twitter Cards](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/abouts-cards)元数据。

### 配置 Twitter Cards 

​	Hugo 的 Twitter Card 模板使用一些配置变量和个别页面的 [front-matter](https://gohugo.io/content-management/front-matter/) 进行混合配置。

config.

=== "yaml"

    ``` yaml
    params:
      description: Text about my cool site
      images:
      - site-feature-image.jpg
    ```

=== "toml"

    ``` toml
    [params]
      description = 'Text about my cool site'
      images = ['site-feature-image.jpg']
    ```

=== "json"

    ``` json
    {
       "params": {
          "description": "Text about my cool site",
          "images": [
             "site-feature-image.jpg"
          ]
       }
    }
    ```

content/blog/my-post.

=== "yaml"

    ``` yaml
    description: Text about this post
    images:
    - post-cover.png
    title: Post title
    ```

=== "toml"

    ``` toml
    description = 'Text about this post'
    images = ['post-cover.png']
    title = 'Post title'
    ```

=== "json"

    ``` json
    {
       "description": "Text about this post",
       "images": [
          "post-cover.png"
       ],
       "title": "Post title"
    }
    ```



​	如果页面的前置元数据中没有指定 `images`，则 Hugo 会搜索具有 `feature`、`cover` 或 `thumbnail` 名称的 [图像页面资源](https://gohugo.io/content-management/image-processing/)。如果找不到具有这些名称的图像资源，则使用在 [站点配置](https://gohugo.io/getting-started/configuration/) 中定义的图像。如果根本找不到图像，则使用不带图像的 Twitter `summary` 卡，而不是 `summary_large_image`。

​	Hugo 使用该页面标题和描述作为卡片的标题和描述字段。如果没有给出描述，则使用该页面摘要。

​	`.Site.Social.twitter` 变量从配置中暴露，作为 `twitter:site` 的值。

config.

=== "yaml"

    ``` yaml
    social:
      twitter: GoHugoIO
    ```

=== "toml"

    ``` toml
    [social]
      twitter = 'GoHugoIO'
    ```

=== "json"

    ``` json
    {
       "social": {
          "twitter": "GoHugoIO"
       }
    }
    ```



注意：`@` 将会自动为您添加。

```html
<meta name="twitter:site" content="@GoHugoIO"/>
```

### 使用 Twitter Cards 模板 

​	要添加 Twitter 卡片元数据，请在您的模板的 `<head>` 元素之后立即包含以下行：

```go-html-template
{{ template "_internal/twitter_cards.html" . }}
```

## 内置模板 

​	这些模板的代码位于[这里](https://github.com/gohugoio/hugo/tree/master/tpl/tplimpl/embedded/templates)。

- `_internal/disqus.html`
- `_internal/google_analytics.html`
- `_internal/google_analytics_async.html`
- `_internal/opengraph.html`
- `_internal/pagination.html`
- `_internal/schema.html`
- `_internal/twitter_cards.html`

## 另请参阅

- [评论](https://gohugo.io/content-management/comments/)
