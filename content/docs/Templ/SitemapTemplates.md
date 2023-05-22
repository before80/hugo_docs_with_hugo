+++
title = "Sitemap模板"
weight = 20
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Sitemap Templates - Sitemap模板 

[https://gohugo.io/templates/sitemap-template/](https://gohugo.io/templates/sitemap-template/)

​	Hugo提供了内置的站点地图（sitemap）模板。 

## 概述 

​	Hugo的内置站点地图模板符合v0.9的[站点地图协议](https://www.sitemaps.org/protocol.html)。

​	对于单语言项目，Hugo将在根目录下使用内置的[sitemap.xml](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/sitemap.xml)模板生成一个sitemap.xml文件，该文件位于[`publishDir`](https://gohugo.io/getting-started/configuration#publishdir)中。

​	对于多语言项目，Hugo会生成：

- 使用内置的[sitemap.xml](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/sitemap.xml)模板，在每个站点（语言）的根目录中生成一个sitemap.xml文件。
- 使用内置的[sitemapindex.xml](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/sitemapindex.xml)模板，在[`publishDir`](https://gohugo.io/getting-started/configuration#publishdir)的根目录中生成一个sitemap.xml文件。

## 配置 

​	在您的站点配置中设置[更改频率](https://www.sitemaps.org/protocol.html#changefreqdef)、[优先级](https://www.sitemaps.org/protocol.html#priority)和生成的文件名称的默认值。

config.

=== "yaml"

    ``` yaml
    sitemap:
      changefreq: monthly
      filename: sitemap.xml
      priority: 0.5
    ```

=== "toml"

    ``` toml
    [sitemap]
      changefreq = 'monthly'
      filename = 'sitemap.xml'
      priority = 0.5
    ```

=== "json"

    ``` json
    {
       "sitemap": {
          "changefreq": "monthly",
          "filename": "sitemap.xml",
          "priority": 0.5
       }
    }
    ```

- changefreq

  页面更改频率的可能性有多大。有效的值包括`always`、`hourly`、`daily`、`weekly`、`monthly`、`yearly`和`never`。默认值为`""`（从渲染的站点地图中省略更改频率）。

- filename

  生成的文件名称。默认值为`sitemap.xml`。

- priority

  相对于站点中的其他页面，该页面的优先级。有效值范围为0.0到1.0。默认值为`-1`（渲染站点地图时省略优先级）。

## 覆盖默认值 

​	在前置元数据中覆盖给定页面的默认值。

news.md

=== "yaml"

    ``` yaml
    ---
    sitemap:
      changefreq: weekly
      priority: 0.8
    title: News
    ---
    ```

=== "toml"

    ``` toml
    +++
    title = 'News'
    [sitemap]
      changefreq = 'weekly'
      priority = 0.8
    +++
    ```

=== "json"

    ``` json
    {
       "sitemap": {
          "changefreq": "weekly",
          "priority": 0.8
       },
       "title": "News"
    }
    ```



## 覆盖内置模板 

​	要覆盖内置的sitemap.xml模板，请在以下任一位置创建一个新文件：

- layouts/sitemap.xml
- layouts/_default/sitemap.xml

​	在对页面集合进行排列时，可以使用`.Sitemap.ChangeFreq`和`.Sitemap.Priority`分别访问*更改频率*和*优先级*。

​	要覆盖内置的sitemapindex.xml模板，请在以下任一位置创建一个新文件：

- layouts/sitemapindex.xml
- layouts/_default/sitemapindex.xml

## 禁用Sitemap生成 

​	您可以在站点配置中禁用站点地图生成：

config.

=== "yaml"

    ``` yaml
    disableKinds:
    - sitemap
    ```

=== "toml"

    ``` toml
    disableKinds = ['sitemap']
    ```

=== "json"

    ``` json
    {
       "disableKinds": [
          "sitemap"
       ]
    }
    ```



## 另请参阅

- [RSS模板 ](https://gohugo.io/templates/rss/)
- [创建自己的简码 ](https://gohugo.io/templates/shortcode-templates/)
- [数据模板 ](https://gohugo.io/templates/data-templates/)
- [Hugo的查找顺序 ](https://gohugo.io/templates/lookup-order/)
- [菜单模板](https://gohugo.io/templates/menu-templates/)
