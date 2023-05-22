+++
title = "Robots.txt"
weight = 21
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Robots.txt File - Robots.txt 文件 

[https://gohugo.io/templates/robots/](https://gohugo.io/templates/robots/)

​	Hugo 可以像任何其他模板一样生成自定义的 robots.txt 文件。 

​	要从模板生成 robots.txt 文件，请更改[站点配置](https://gohugo.io/getting-started/configuration/)：

config.

=== "yaml"

    ``` yaml
    enableRobotsTXT: true
    ```

=== "toml"

    ``` toml
    enableRobotsTXT = true
    ```

=== "json"

    ``` json
    {
       "enableRobotsTXT": true
    }
    ```

​	默认情况下，Hugo使用[内置模板](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/robots.txt)生成 robots.txt。

```text
User-agent: *
```

​	遵守Robots Exclusion Protocol的搜索引擎将把这个文件解释为允许爬取站点上的所有内容。

## Robots.txt 模板查找顺序 

​	您可以使用自定义模板覆盖内置模板。Hugo使用以下查找顺序选择模板：

1. `/layouts/robots.txt`
2. `/themes/<THEME>/layouts/robots.txt`

## Robots.txt 模板示例

layouts/robots.txt

```txt
User-agent: *
{{ range .Pages }}
Disallow: {{ .RelPermalink }}
{{ end }}
```

​	该模板将为站点上的每个页面创建一个 robots.txt 文件，使用`Disallow`指令。遵守Robots Exclusion Protocol的搜索引擎将不会爬取站点上的任何页面。

​	要创建一个不使用模板的 robots.txt 文件：

1. 在[站点配置](https://gohugo.io/getting-started/configuration/)中将 `enableRobotsTXT` 设置为 `false`。
2. 在 `static` 目录中创建一个 robots.txt 文件。

​	请记住，Hugo在构建站点时将 [static 目录](https://gohugo.io/getting-started/directory-structure/) 中的所有内容复制到 `publishDir` (通常为 `public`) 的根目录。
