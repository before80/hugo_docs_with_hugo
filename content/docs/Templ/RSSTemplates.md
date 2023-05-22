+++
title = "RSS模板"
weight = 19
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# RSS Templates - RSS模板 

[https://gohugo.io/templates/rss/](https://gohugo.io/templates/rss/)

​	Hugo 自带 RSS 2.0 模板，几乎不需要配置，或者您可以创建自己的 RSS 模板。 

## RSS模板查找顺序 

​	有关完整参考，请参见 [Template Lookup Order](https://gohugo.io/templates/lookup-order/)。

​	Hugo 自带了 [RSS 2.0 模板](https://gohugo.io/templates/rss/#the-embedded-rssxml)。嵌入式模板对于大多数用例已经足够了。

​	RSS 页面属于 `Page` 类型，并且在模板中可以使用所有 [页面变量](https://gohugo.io/variables/page/)。

### Section RSS 

​	[section](https://gohugo.io/content-management/sections/) 的 RSS 将在 `/<SECTION>/index.xml`（例如，[https://spf13.com/project/index.xml](https://spf13.com/project/index.xml)）处被渲染。

​	Hugo 提供了定义任何 RSS 类型的功能，并且可以为每个章节和分类法设置不同的 RSS 文件。

## RSS模板查找顺序表 

​	下表显示了不同页面类型的 RSS 模板查找顺序。第一个列表显示了在使用某一主题（`demoTheme`）运行时的查找顺序。

| Example                | OutputFormat | 后缀 | Template Lookup Order                                        |
| :--------------------- | :----------- | :--- | :----------------------------------------------------------- |
| RSS home               | RSS          | xml  | 1. layouts/index.rss.xml<br/>2. layouts/home.rss.xml<br/>3. layouts/rss.xml<br/>4. layouts/list.rss.xml<br/>5. layouts/index.xml<br/>6. layouts/home.xml<br/>7. layouts/list.xml<br/>8. layouts/_default/index.rss.xml<br/>9. layouts/_default/home.rss.xml<br/>10. layouts/_default/rss.xml<br/>11. layouts/_default/list.rss.xml<br/>12. layouts/_default/index.xml<br/>13. layouts/_default/home.xml<br/>14. layouts/_default/list.xml<br/>15. layouts/_internal/_default/rss.xml |
| RSS section posts      | RSS          | xml  | 1. layouts/posts/section.rss.xml<br/>2. layouts/posts/rss.xml<br/>3. layouts/posts/list.rss.xml<br/>4. layouts/posts/section.xml<br/>5. layouts/posts/list.xml<br/>6. layouts/section/section.rss.xml<br/>7. layouts/section/rss.xml<br/>8. layouts/section/list.rss.xml<br/>9. layouts/section/section.xml<br/>10. layouts/section/list.xml<br/>11. layouts/_default/section.rss.xml<br/>12. layouts/_default/rss.xml<br/>13. layouts/_default/list.rss.xml<br/>14. layouts/_default/section.xml<br/>15. layouts/_default/list.xml<br/>16. layouts/_internal/_default/rss.xml |
| Taxonomy in categories | RSS          | xml  | 1. layouts/categories/category.terms.rss.xml<br/>2. layouts/categories/terms.rss.xml<br/>3. layouts/categories/taxonomy.rss.xml<br/>4. layouts/categories/rss.xml<br/>5. layouts/categories/list.rss.xml<br/>6. layouts/categories/category.terms.xml<br/>7. layouts/categories/terms.xml<br/>8. layouts/categories/taxonomy.xml<br/>9. layouts/categories/list.xml<br/>10. layouts/category/category.terms.rss.xml<br/>11. layouts/category/terms.rss.xml<br/>12. layouts/category/taxonomy.rss.xml<br/>13. layouts/category/rss.xml<br/>14. layouts/category/list.rss.xml<br/>15. layouts/category/category.terms.xml<br/>16. layouts/category/terms.xml<br/>17. layouts/category/taxonomy.xml<br/>18. layouts/category/list.xml<br/>19. layouts/taxonomy/category.terms.rss.xml<br/>20. layouts/taxonomy/terms.rss.xml<br/>21. layouts/taxonomy/taxonomy.rss.xml<br/>22. layouts/taxonomy/rss.xml<br/>23. layouts/taxonomy/list.rss.xml<br/>24. layouts/taxonomy/category.terms.xml<br/>25. layouts/taxonomy/terms.xml<br/>26. layouts/taxonomy/taxonomy.xml<br/>27. layouts/taxonomy/list.xml<br/>28. layouts/_default/category.terms.rss.xml<br/>29. layouts/_default/terms.rss.xml<br/>30. layouts/_default/taxonomy.rss.xml<br/>31. layouts/_default/rss.xml<br/>32. layouts/_default/list.rss.xml<br/>33. layouts/_default/category.terms.xml<br/>34. layouts/_default/terms.xml<br/>35. layouts/_default/taxonomy.xml<br/>36. layouts/_default/list.xml<br/>37. layouts/_internal/_default/rss.xml |
| Term in categories     | RSS          | xml  | 1. layouts/categories/term.rss.xml<br/>2. layouts/categories/category.rss.xml<br/>3. layouts/categories/taxonomy.rss.xml<br/>4. layouts/categories/rss.xml<br/>5. layouts/categories/list.rss.xml<br/>6. layouts/categories/term.xml<br/>7. layouts/categories/category.xml<br/>8. layouts/categories/taxonomy.xml<br/>9. layouts/categories/list.xml<br/>10. layouts/term/term.rss.xml<br/>11. layouts/term/category.rss.xml<br/>12. layouts/term/taxonomy.rss.xml<br/>13. layouts/term/rss.xml<br/>14. layouts/term/list.rss.xml<br/>15. layouts/term/term.xml<br/>16. layouts/term/category.xml<br/>17. layouts/term/taxonomy.xml<br/>18. layouts/term/list.xml<br/>19. layouts/taxonomy/term.rss.xml<br/>20. layouts/taxonomy/category.rss.xml<br/>21. layouts/taxonomy/taxonomy.rss.xml<br/>22. layouts/taxonomy/rss.xml<br/>23. layouts/taxonomy/list.rss.xml<br/>24. layouts/taxonomy/term.xml<br/>25. layouts/taxonomy/category.xml<br/>26. layouts/taxonomy/taxonomy.xml<br/>27. layouts/taxonomy/list.xml<br/>28. layouts/category/term.rss.xml<br/>29. layouts/category/category.rss.xml<br/>30. layouts/category/taxonomy.rss.xml<br/>31. layouts/category/rss.xml<br/>32. layouts/category/list.rss.xml<br/>33. layouts/category/term.xml<br/>34. layouts/category/category.xml<br/>35. layouts/category/taxonomy.xml<br/>36. layouts/category/list.xml<br/>37. layouts/_default/term.rss.xml<br/>38. layouts/_default/category.rss.xml<br/>39. layouts/_default/taxonomy.rss.xml<br/>40. layouts/_default/rss.xml<br/>41. layouts/_default/list.rss.xml<br/>42. layouts/_default/term.xml<br/>43. layouts/_default/category.xml<br/>44. layouts/_default/taxonomy.xml<br/>45. layouts/_default/list.xml<br/>46. layouts/_internal/_default/rss.xml |





## 配置RSS 

​	默认情况下，Hugo 将创建无限数量的 RSS 条目。您可以通过在项目的 [`config` 文件](https://gohugo.io/getting-started/configuration/) 中分配数值给 `rssLimit:` 字段来限制内置 RSS 模板中包含的文章数量。

​	如果指定以下值，它们也将包含在 RSS 输出中：

config.

=== "yaml"

    ``` yaml
    author:
      name: My Name Here
    copyright: This work is licensed under a Creative Commons Attribution-ShareAlike 4.0
      International License.
    languageCode: en-us
    ```

=== "toml"

    ``` toml
    copyright = 'This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.'
    languageCode = 'en-us'
    [author]
      name = 'My Name Here'
    ```

=== "json"

    ``` json
    {
       "author": {
          "name": "My Name Here"
       },
       "copyright": "This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.",
       "languageCode": "en-us"
    }
    ```



## 内嵌的rss.xml 

​	以下是 Hugo 自带的默认 RSS 模板：

[https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/rss.xml](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/rss.xml)

## 在`<head>`中引用RSS 订阅 

​	在您的 `header.html` 模板中，您可以使用 Hugo 的 [输出格式](https://gohugo.io/templates/output-formats/#link-to-output-formats) 在 `<head></head>` 标签中指定您的 RSS 订阅，如下所示：

```go-html-template
{{ range .AlternativeOutputFormats -}}
    {{ printf `<link rel="%s" type="%s" href="%s" title="%s" />` .Rel .MediaType.Type .Permalink $.Site.Title | safeHTML }}
{{ end -}}
```

​	如果您只想要 RSS 链接，则可以查询该格式：

```go-html-template
{{ with .OutputFormats.Get "rss" -}}
    {{ printf `<link rel="%s" type="%s" href="%s" title="%s" />` .Rel .MediaType.Type .Permalink $.Site.Title | safeHTML }}
{{ end -}}
```

​	上述两个片段中的任何一个都将为站点首页生成以下 `link` 标记以用于 RSS 输出：

```html
<link rel="alternate" type="application/rss+xml" href="https://example.com/index.xml" title="Site Title">
```

​	*在本示例中，我们假设 `BaseURL` 为 `https://example.com/`，`$.Site.Title` 为 `"Site Title"`。*

## 另请参阅 

- [Sitemap模板 ](https://gohugo.io/templates/sitemap-template/)
- [创建自己的简码 ](https://gohugo.io/templates/shortcode-templates/)
- [自定义输出格式 ](https://gohugo.io/templates/output-formats/)
- [数据模板 ](https://gohugo.io/templates/data-templates/)
- [Hugo的查找顺序](https://gohugo.io/templates/lookup-order/)
