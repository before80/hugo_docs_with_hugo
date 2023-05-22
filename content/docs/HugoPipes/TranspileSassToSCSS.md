+++
title = "ToCSS"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# ToCSS

[https://gohugo.io/hugo-pipes/transform-to-css/](https://gohugo.io/hugo-pipes/transform-to-css/)

​	将 Sass 转译为 CSS。  

## 语法

```
resources.ToCSS RESOURCE [OPTIONS]
toCSS RESOURCE [OPTIONS]
```

## 用法

​	可以使用  `resources.ToCSS`  将任何 Sass 或 SCSS 文件转换为 CSS 文件，其中需要两个参数：资源对象和下面列出的一个选项映射。

```go-html-template
{{ $sass := resources.Get "sass/main.scss" }}
{{ $style := $sass | resources.ToCSS }}
```

### 选项

- transpiler [string]

  使用的  `transpiler` ，有效值为  `libsass` （默认）和  `dartsass` 。如果您想使用 Hugo 与 Dart Sass，请从 [Embedded Dart Sass](https://github.com/sass/dart-sass-embedded/releases) 下载发布二进制文件，并确保它在您的 PC 的  `$PATH` （或 Windows 上的  `%PATH%` ）中。  

- targetPath [string]

  如果未设置，则转换后的资源的目标路径将是asset文件原始路径，其扩展名将替换为  `.css` 。  

- vars [map]

  键/值对的映射，将在  `hugo:vars`  命名空间中可用，例如：使用  `@use "hugo:vars" as v;`  或（全局）使用  `@import "hugo:vars";` 。[自 v0.109.0 起新增](https://github.com/gohugoio/hugo/releases/tag/v0.109.0) 

- outputStyle [string]

  默认值为  `nested` （LibSass）和  `expanded` （Dart Sass）。LibSass 的其他可用输出样式为  `expanded` 、 `compact`  和  `compressed` 。Dart Sass 仅支持  `expanded`  和  `compressed` 。  

- precision [int]

  浮点数精度。**注意**：Dart Sass 不支持此选项。  

- enableSourceMap [bool]

  启用时，将生成源映射。  

- sourceMapIncludeSources [bool]

  启用时，源将嵌入到生成的源映射中。（仅在 Dart Sass 中）。[自 v0.108.0 起新增](https://github.com/gohugoio/hugo/releases/tag/v0.108.0) 

- includePaths [string slice]

  额外的 SCSS/Sass 包含路径。路径必须相对于项目目录。

```go-html-template
{{ $options := (dict "targetPath" "style.css" "outputStyle" "compressed" "enableSourceMap" (not hugo.IsProduction) "includePaths" (slice "node_modules/myscss")) }}
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS $options }}
```

​	将  `outputStyle`  设置为  `compressed`  将比更通用的 [ `resources.Minify`](https://gohugo.io/hugo-pipes/minification) 更好地处理 Sass/SCSS 文件的压缩。  

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [js.Build](https://gohugo.io/hugo-pipes/js/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
- [Fingerprint](https://gohugo.io/hugo-pipes/fingerprint/)
