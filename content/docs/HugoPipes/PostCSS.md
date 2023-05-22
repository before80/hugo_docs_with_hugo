+++
title = "PostCSS"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# PostCSS

[https://gohugo.io/hugo-pipes/postcss/](https://gohugo.io/hugo-pipes/postcss/)

​	使用任何可用的插件，使用PostCSS处理CSS文件。  

## 语法

```
resources.PostCSS RESOURCE [OPTIONS]
postCSS RESOURCE [OPTIONS]
```

## 设置 

​	按照以下步骤使用任何[可用的PostCSS插件](https://www.postcss.parts/)来转换CSS。 

- Step 1

  安装 [Node.js](https://nodejs.org/en/download).

- Step 2

  在项目的根目录中安装所需的Node.js包。例如，添加vendor 前缀到CSS规则：

```bash
npm install postcss postcss-cli autoprefixer
```

- Step 3

  在项目的根目录中创建PostCSS配置文件。您必须将此文件命名为  `postcss.config.js`  或其他[supported file names](https://github.com/postcss/postcss-load-config#usage)之一。例如： 

postcss.config.js

```js
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
};
```

​	如果您是Windows用户，且项目路径包含空格，则必须将PostCSS配置放置在package.json文件中。参见[此示例](https://github.com/postcss/postcss-load-config#packagejson)和问题[#7333](https://github.com/gohugoio/hugo/issues/7333)。 

- Step 4

  将CSS文件放置在  `assets`  目录中。 

- Step 5

  将CSS文件作为资源捕获，并通过 `resources.PostCSS` （别名 `postCSS` ）进行管道处理： 

layouts/partials/css.html

```go-html-template
{{ with resources.Get "css/main.css" | postCSS }}
  <link rel="stylesheet" href="{{ .RelPermalink }}">
{{ end }}
```

​	如果在  `assets`  目录中使用Sass文件：  

layouts/partials/css.html

```go-html-template
{{ with resources.Get "sass/main.scss" | toCSS | postCSS }}
  <link rel="stylesheet" href="{{ .RelPermalink }}">
{{ end }}
```

## 选项

 	`resources.PostCSS`  方法接受一个可选的选项映射。  

- config

  ( `string` ) 包含PostCSS配置文件的目录。默认为项目目录的根目录。  

- noMap

  ( `bool` ) 默认为  `false` 。如果为  `true` ，则禁用内联源地图（sourcemaps）。  

- inlineImports

  ( `bool` ) 默认为  `false` 。启用@import语句的内联。它会递归执行，但只会导入一次文件。URL导入（例如  `@import 
  url('https://fonts.googleapis.com/css?family=Open+Sans&display=swap');` ）和带媒体查询的导入将被忽略。请注意，此导入例程不关心CSS规范，因此您可以在文件中的任何地方使用@import。Hugo将查找相对于模块挂载的导入并遵守主题覆盖。 

- skipInlineImportsNotFound [New in v0.99.0](https://github.com/gohugoio/hugo/releases/tag/v0.99.0)

    ( `bool` ) 默认为  `false` 。在Hugo 0.99.0之前，当启用 `inlineImports` 并且我们无法解析导入时，我们会将其记录为警告。现在我们将构建失败。如果您的CSS中有常规CSS导入要保留，则可以使用带URL的导入或媒体查询（Hugo不会尝试解决这些导入），或将 `skipInlineImportsNotFound` 设置为true。  

layouts/partials/css.html

```go-html-template
{{ $opts := dict "config" "config-directory" "noMap" true }}
{{ with resources.Get "css/main.css" | postCSS $opts }}
  <link rel="stylesheet" href="{{ .RelPermalink }}">
{{ end }}
```

## 无配置文件  

​	为了避免使用PostCSS配置文件，可以使用选项映射指定最小的配置。  

- use

  (`string`) 用于指定要使用的 PostCSS 插件的以空格分隔的列表。 

- parser

  (`string`) 自定义 PostCSS 解析器。 

- stringifier

  (`string`) 自定义 PostCSS 字符串化器。 

- syntax

  (`string`) 自定义 PostCSS 语法。

layouts/partials/css.html

```go-html-template
{{ $opts := dict "use" "autoprefixer postcss-color-alpha" }}
{{ with resources.Get "css/main.css" | postCSS $opts }}
  <link rel="stylesheet" href="{{ .RelPermalink }}">
{{ end }}
```

## 检查 Hugo 环境

​	当前的 Hugo 环境名称（通过 `--environment` 在配置或操作系统环境中设置）在 Node 上下文中可用，这使得可以使用如下结构：

postcss.config.js

```js
module.exports = {
  plugins: [
    require('autoprefixer'),
    ...process.env.HUGO_ENVIRONMENT === 'production'
      ? [purgecss]
      : []
  ]
}
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Host on 21YunBox](https://gohugo.io/hosting-and-deployment/hosting-on-21yunbox/)
- [ToCSS](https://gohugo.io/hugo-pipes/transform-to-css/)
- [highlight](https://gohugo.io/functions/highlight/)
- [hugo](https://gohugo.io/commands/hugo/)
