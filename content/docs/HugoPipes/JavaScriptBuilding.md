+++
title = "js.Build"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# js.Build

[https://gohugo.io/hugo-pipes/js/](https://gohugo.io/hugo-pipes/js/)

​	使用 [ESBuild](https://github.com/evanw/esbuild) 处理一个 JavaScript 文件。  

## 语法

```
js.Build RESOURCE [OPTIONS]
```

## 用法 

​	任何 JavaScript 资源文件都可以使用  `js.Build`  进行转换和 "tree shaken"，其参数可以是文件路径的字符串，也可以是下面列出的选项字典。  

### 选项 

- targetPath [string]

  如果未设置，则使用源路径作为基本目标路径。请注意，如果目标 MIME 类型不同，目标路径的扩展名可能会更改，例如，当源是 TypeScript 时。  

- params [map or slice]

  可以在 JS 文件中作为 JSON 导入的参数，例如：

```go-html-template
{{ $js := resources.Get "js/main.js" | js.Build (dict "params" (dict "api" "https://example.org/api")) }}
```

​	然后在您的 JS 文件中：

```js
import * as params from '@params';
```

​	请注意，这适用于小型数据集，例如配置设置。对于较大的数据，请将文件放置/挂载到  `/assets`  中并直接导入它们。  

- minify [bool]

  让  `js.Build`  处理最小化。  

- inject [slice]

  此选项允许您自动将另一个文件中的导入替换为全局变量。路径名必须相对于  `assets` 。 参考 [https://esbuild.github.io/api/#inject](https://esbuild.github.io/api/#inject ) 

- shims [map]

  此选项允许将一个组件替换为另一个组件。常见的用例是在生产环境中从 CDN（带有*shims*）加载依赖项（如 React），但在开发期间使用完全捆绑的 `node_modules` 依赖项：

```go-html-template
{{ $shims := dict "react" "js/shims/react.js"  "react-dom" "js/shims/react-dom.js" }}
{{ $js = $js | js.Build dict "shims" $shims }}
```

​	这些 *shim* 文件可能是这样的：

```js
// js/shims/react.js
module.exports = window.React;
// js/shims/react-dom.js
module.exports = window.ReactDOM;
```

​	使用上述方法，以下导入应该在两种情况下都能正常工作：

```js
import * as React from 'react'
import * as ReactDOM from 'react-dom';
```

- target [string]

  语言目标。可选值为： `es5` ， `es2015` ， `es2016` ， `es2017` ， `es2018` ， `es2019` ， `es2020` 或 `esnext` 。 默认为  `esnext` 。  

- externals [slice]

  外部依赖项。使用此选项来修剪您知道永远不会执行的依赖项。 参考[https://esbuild.github.io/api/#external](https://esbuild.github.io/api/#external) 

- defines [map]

   允许定义（在构建时执行）一组字符串替换。应该是一个 map，其中每个键都将被其值替换。

```go-html-template
{{ $defines := dict "process.env.NODE_ENV" `"development"` }}
```

- format [string]

  输出格式。可选值为： `iife` ， `cjs` ， `esm` 。默认为 `iife` ，一个适合作为标签（tag）包含的自执行函数。

- sourceMap [string]

  是否从 esbuild 生成  `inline`  或  `external`  源映射。外部源映射将写入目标输出文件名 + ".map"。输入源映射可以从 js.Build 和节点模块中读取并合并到输出源映射中。默认情况下，不创建源映射。  

### 从 /assets 导入 JS 代码 

​	`js.Build`  完全支持 [Hugo Modules](https://gohugo.io/hugo-modules/) 中的虚拟并联文件系统。您可以在这个 [测试项目](https://github.com/gohugoio/hugoTestProjectJSModImports) 中看到一些简单的示例，但简而言之，您可以这样做：

```js
import { hello } from 'my/module';
```

​	它将解析为分层文件系统中`assets/my/module`下最顶层的 `index.{js,ts,tsx,jsx}` 文件。

```js
import { hello3 } from 'my/module/hello3';
```

​	将解析为  `assets/my/module`  中的  `hello3.{js,ts,tsx,jsx}` 。  

​	任何以  `.`  开头的导入都将相对于当前文件进行解析：

```js
import { hello4 } from './lib';
```

​	对于其他文件（例如 `JSON`，`CSS`），您需要使用包括任何扩展名在内的相对路径，例如：

```js
import * as data from 'my/module/data.json';
```

​	在位于 `/assets` 之外或不能解析为 `/assets` 内组件的文件中的任何导入都将由 [ESBuild](https://esbuild.github.io/) 解析，并将 **项目目录** 作为解析目录（用作查找 `node_modules` 等的起始点）。另请参见[hugo mod npm pack](https://gohugo.io/commands/hugo_mod_npm_pack/)。如果在项目中导入了任何 npm 依赖项，则需要在运行 `hugo` 之前确保运行 `npm install`。

​	此外，请注意新的 `params` 选项，它可以从模板传递到您的 JS 文件中，例如：

```go-html-template
{{ $js := resources.Get "js/main.js" | js.Build (dict "params" (dict "api" "https://example.org/api")) }}
```

​	然后在您的 JS 文件中：

```js
import * as params from '@params';
```

​	Hugo 默认会生成一个  `assets/jsconfig.json`  文件来映射导入。这对于代码编辑器中的导航/智能感知帮助很有用，但是如果您不需要/不想要它，您可以 [关闭它](https://gohugo.io/getting-started/configuration/#configure-build)。 

### 将依赖项包含在 package.json / node_modules 中 

​	在位于 `/assets` 之外或不能解析为 `/assets` 内组件的文件中的任何导入都将由 [ESBuild](https://esbuild.github.io/) 解析，并将 **项目目录** 作为解析目录（用作查找 `node_modules` 等的起始点）。另请参见[hugo mod npm pack](https://gohugo.io/commands/hugo_mod_npm_pack/)。如果在项目中导入了任何 npm 依赖项，则需要在运行 `hugo` 之前确保运行 `npm install`。

​	解析 npm 包（即位于 `node_modules` 文件夹中的包）的起始目录始终是主项目文件夹。

**注意：**如果您正在开发应该被导入并且依赖于 `package.json` 内的依赖项的主题/组件，我们建议了解 [hugo mod npm pack](https://gohugo.io/commands/hugo_mod_npm_pack/)，这是一种将项目中所有 npm 依赖项合并的工具。

### 示例 

```go-html-template
{{ $built := resources.Get "js/index.js" | js.Build "main.js" }}
```

或者带有选项：

```go-html-template
{{ $externals := slice "react" "react-dom" }}
{{ $defines := dict "process.env.NODE_ENV" `"development"` }}

{{ $opts := dict "targetPath" "main.js" "externals" $externals "defines" $defines }}
{{ $built := resources.Get "scripts/main.js" | js.Build $opts }}
<script src="{{ $built.RelPermalink }}" defer></script>
```

## 另请参阅

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [ToCSS](https://gohugo.io/hugo-pipes/transform-to-css/)
- [highlight](https://gohugo.io/functions/highlight/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
