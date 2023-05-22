+++
title = "相关内容"
weight = 10
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Related Content - 相关内容 

[https://gohugo.io/content-management/related/](https://gohugo.io/content-management/related/)

​	在"另请参阅"章节中列出相关内容。 

​	Hugo 使用一组因素来基于前置元数据参数识别页面的相关内容。这可以调整为所需的索引和参数集，或者留给Hugo的默认[相关内容配置](https://gohugo.io/content-management/related/#configure-related-content)。

## 列出相关内容 

​	要列出最多 5 个相关页面（共享相同的*date*或*keyword*参数），只需在您的单个页面模板中包含类似以下内容的partial：

layouts/partials/related.html

```go-html-template
{{ $related := .Site.RegularPages.Related . | first 5 }}
{{ with $related }}
<h3>See Also</h3>
<ul>
 {{ range . }}
 <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
 {{ end }}
</ul>
{{ end }}
```

​	`Related`方法接受一个参数，可以是`Page`或选项映射。这些选项映射具有以下选项：

- indices

  要搜索的索引。 

- document

  要搜索相关内容的文档。 

- namedSlices

  要搜索的关键字。 

- fragments

  片段（fragments ）包含一个用于配置为"fragments"类型的索引的特殊关键字列表。这将匹配文档的片段（fragment ）标识符。

​	使用以上所有选项的虚构示例：

```go-html-template
{{ $page := . }}
{{ $opts := 
  "indices" (slice "tags" "keywords")
  "document" $page
  "namedSlices" (slice (keyVals "tags" "hugo" "rocks") (keyVals "date" $page.Date))
  "fragments" (slice "heading-1" "heading-2")
}}
```

> ​	我们在Hugo 0.111.0中改进和简化了这个功能。在此之前，我们有3种不同的方法：`Related`，`RelatedTo`和`RelatedIndicies`。现在我们只有一个方法：`Related`。旧的方法仍然可用但已弃用。另请参阅[此博客文章](https://regisphilibert.com/blog/2018/04/hugo-optmized-relashionships-with-related-content/)，以获得更高级用法的详细解释。

## 在相关内容中索引内容标题 

[New in v0.111.0](https://github.com/gohugoio/hugo/releases/tag/v0.111.0)

​	Hugo可以索引您内容中的标题，并使用此功能查找相关内容。您可以通过将类型为`fragments`的索引添加到`related`配置中来启用此功能：

config.

=== "yaml"

    ``` yaml
    related:
      includeNewer: true
      indices:
      - applyFilter: false
        name: fragmentrefs
        type: fragments
        weight: 80
      threshold: 20
      toLower: false
    ```

=== "toml"

    ``` toml
    [related]
      includeNewer = true
      threshold = 20
      toLower = false
    [[related.indices]]
      applyFilter = false
      name = 'fragmentrefs'
      type = 'fragments'
      weight = 80
    ```

=== "json"

    ``` json
    {
       "related": {
          "includeNewer": true,
          "indices": [
             {
                "applyFilter": false,
                "name": "fragmentrefs",
                "type": "fragments",
                "weight": 80
             }
          ],
          "threshold": 20,
          "toLower": false
       }
    }
    ```



- `name`映射到可选的前置元数据切片属性，可用于从页面级别链接到片段/标题（fragment/heading）级别。 
- 如果启用`applyFilter`，则结果中每个页面上的`.HeadingsFiltered`将反映筛选后的标题。如果您想在相关内容列表中显示标题，则这很有用： 

```go-html-template
{{ $related := .Site.RegularPages.Related . | first 5 }}
{{ with $related }}
  <h2>See Also</h2>
  <ul>
    {{ range $i, $p := . }}
      <li>
        <a href="{{ .RelPermalink }}">{{ .Title }}</a>
        {{ with .HeadingsFiltered }}
          <ul>
            {{ range . }}
              {{ $link := printf "%s#%s" $p.RelPermalink .ID | safeURL }}
              <li>
                <a href="{{ $link }}">{{ .Title }}</a>
              </li>
            {{ end }}
          </ul>
        {{ end }}
      </li>
    {{ end }}
  </ul>
{{ end }}
```

## 配置相关内容 

​	Hugo提供了相关内容的合理默认配置，但是如果需要，您可以在全局或语言级别上对其进行微调。

### 默认配置 

​	如果项目上没有设置任何`related`配置，则Hugo的相关内容方法将使用以下内容。

config.

=== "yaml"

    ``` yaml
    related:
      includeNewer: false
      indices:
      - name: keywords
        weight: 100
      - name: date
        weight: 10
      threshold: 80
      toLower: false
    ```

=== "toml"

    ``` toml
    [related]
      includeNewer = false
      threshold = 80
      toLower = false
    [[related.indices]]
      name = 'keywords'
      weight = 100
    [[related.indices]]
      name = 'date'
      weight = 10
    ```

=== "json"

    ``` json
    {
       "related": {
          "includeNewer": false,
          "indices": [
             {
                "name": "keywords",
                "weight": 100
             },
             {
                "name": "date",
                "weight": 10
             }
          ],
          "threshold": 80,
          "toLower": false
       }
    }
    ```



​	请注意，如果您将`tags`配置为分类（taxonomy），那么`tags`将与上述默认配置一起添加，并且权重为`80`。

​	应该使用相同的语法设置自定义配置。

> 如果添加了一个`related` 配置部分，则需要添加完整配置。不能只设置例如 `includeNewer`，并使用 Hugo 默认值中的其他部分。

### 顶级配置选项 

- threshold

  0-100之间的值。较低的值将提供更多但可能不是很相关的匹配项。 

- includeNewer

  设置为`true`以在相关内容列表中包含新于当前页面的页面。这意味着旧帖子的输出可能会随着添加新的相关内容而发生变化。 

- toLower

  将索引和查询中的关键字转换为小写。这可能会以轻微的性能损失为代价提供更准确的结果。请注意，这也可以针对每个索引进行设置。

### 每个索引的配置选项 

- name

  索引名称。此值直接映射到页面参数。 Hugo支持字符串值（例如示例中的`author`）和列表（`tags`，`keywords`等）以及时间和日期对象。 

- type

  [v0.111.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.111.0)的新功能。`basic`（默认）或`fragments`之一。 

- applyFilter

  [v0.111.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.111.0)的新功能。将`type`特定的过滤器应用于搜索结果。目前仅用于`fragments`类型。  

- weight

  表示该参数相对于其他参数的重要性的整数权重。它可以是0，这将关闭此索引的效果，甚至可以是负数。使用不同的值进行测试，以确定最适合您内容的值。 

- cardinalityThreshold (default 0)

  [v0.111.0 中](https://github.com/gohugoio/hugo/releases/tag/v0.111.0)的新功能。用于从索引中删除常见关键字的百分比（0-100）。例如，将此设置为50将删除在索引中使用超过50％的文档中使用的所有关键字。 

- pattern

  目前仅对日期相关。在列出相关内容时，我们可能希望列出时间上也接近的内容。将"2006"（日期索引的默认值）设置为日期索引的模式将增加发布于同一年的页面的权重。对于访问频繁的博客，"200601"（年份和月份）可能是更好的默认值。 

- toLower

  见上文。 

## 性能考虑 

​	快是Hugo的中间名，如果它不是非常快，我们不会发布此功能。

​	这个功能已经在后台计划中，并被很多人长期要求。这个开发最近受到这个Twitter帖子的推动：

<iframe id="twitter-widget-0" scrolling="no" frameborder="0" allowtransparency="true" allowfullscreen="true" class="" title="Twitter Tweet" src="https://platform.twitter.com/embed/Tweet.html?dnt=false&amp;embedId=twitter-widget-0&amp;features=eyJ0ZndfdGltZWxpbmVfbGlzdCI6eyJidWNrZXQiOltdLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2ZvbGxvd2VyX2NvdW50X3N1bnNldCI6eyJidWNrZXQiOnRydWUsInZlcnNpb24iOm51bGx9LCJ0ZndfdHdlZXRfZWRpdF9iYWNrZW5kIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd19yZWZzcmNfc2Vzc2lvbiI6eyJidWNrZXQiOiJvbiIsInZlcnNpb24iOm51bGx9LCJ0ZndfbWl4ZWRfbWVkaWFfMTU4OTciOnsiYnVja2V0IjoidHJlYXRtZW50IiwidmVyc2lvbiI6bnVsbH0sInRmd19leHBlcmltZW50c19jb29raWVfZXhwaXJhdGlvbiI6eyJidWNrZXQiOjEyMDk2MDAsInZlcnNpb24iOm51bGx9LCJ0ZndfZHVwbGljYXRlX3NjcmliZXNfdG9fc2V0dGluZ3MiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3ZpZGVvX2hsc19keW5hbWljX21hbmlmZXN0c18xNTA4MiI6eyJidWNrZXQiOiJ0cnVlX2JpdHJhdGUiLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2xlZ2FjeV90aW1lbGluZV9zdW5zZXQiOnsiYnVja2V0Ijp0cnVlLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3R3ZWV0X2VkaXRfZnJvbnRlbmQiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfX0%3D&amp;frame=false&amp;hideCard=false&amp;hideThread=false&amp;id=898398437527363585&amp;lang=en&amp;origin=https%3A%2F%2Fgohugo.io%2Fcontent-management%2Frelated%2F&amp;sessionId=48abe00a23fa456a3c0546b394cc6d67c940b68c&amp;siteScreenName=GoHugoIO&amp;theme=light&amp;widgetsVersion=aaf4084522e3a%3A1674595607486&amp;width=550px" data-tweet-id="898398437527363585" style="visibility: visible; width: 544px; height: 321px; display: block; flex-grow: 1;"></iframe>

​	Scott S. Lowe 移除了使用标签上的`intersect`模板函数构建的"相关内容"部分，结果在其拥有 1700 篇文章的博客上，构建时间从 30 秒减少到不到 2 秒。

​	他现在应该能够添加一个改进版的"相关内容"部分，而不会影响快速的实时重新加载。但需要注意的是：

​	他现在应该能够添加改进版的"相关内容"部分，而不放弃快速的实时重载。但值得注意的是：

- 如果您不使用任何`Related`方法，您将不会使用相关内容功能，性能将与之前相同。 
- 调用`.RegularPages.Related`等将创建一个倒排索引（有时也称为posting list），它将被重用于同一页面集合中的任何查找。在另外调用`.Pages.Related`之类的方法时，它会按预期工作，但会创建一个额外的倒排索引。这仍然非常快，但值得注意，特别是对于较大的站点。 

> ​	我们目前不对页面内容进行索引。我们认为在解决 [Sherlock 的最后一个案件](https://github.com/joearms/sherlock)之前，发布一些能让大多数人满意的东西是值得的。

## 另请参阅 

- [构建选项 ](https://gohugo.io/content-management/build-options/)
- [评论](https://gohugo.io/content-management/comments/)
- [内容组织 ](https://gohugo.io/content-management/organization/)
- [页面资源 ](https://gohugo.io/content-management/page-resources/)
- [简码](https://gohugo.io/content-management/shortcodes/)
