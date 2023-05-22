+++
title = "Babel"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Babel

[https://gohugo.io/hugo-pipes/babel/](https://gohugo.io/hugo-pipes/babel/)

​	Hugo Pipes 可以使用 Babel 处理 JS 文件。  

## 语法

```
resources.Babel RESOURCE [OPTIONS]
babel RESOURCE [OPTIONS]
```

## 用法 

​	使用  `resources.Babel`  将任何 JavaScript 资源文件转译为另一种 JavaScript 版本，它接受资源对象和下面列出的可选选项字典作为参数。Babel 使用 [babel cli](https://babeljs.io/docs/en/babel-cli)。 

​	Hugo Pipe 的 Babel 需要安装 `@babel/cli` 和 `@babel/core` JavaScript 包在项目中或全局安装 (`npm install -g @babel/cli @babel/core`)，以及使用的任何 Babel 插件或预设 (例如，`npm install @babel/preset-env --save-dev`)。

​	如果您使用的是 Hugo Snap 包，则 Babel 和插件需要在您的 Hugo 站点目录中本地安装，例如，不带 `-g` 标志的 `npm install @babel/cli @babel/core --save-dev`。

### 配置

​	当运行 Babel 和类似工具时，我们会将主项目的 `node_modules` 添加到 `NODE_PATH`。在这个领域，Babel 存在一些已知[问题](https://github.com/babel/babel/issues/5618)，因此如果您的 `babel.config.js` 存在于 Hugo 模块中（而不是项目本身），我们建议使用 `require` 来加载预设/插件，例如：

```js
module.exports = {
  presets: [
    [
      require("@babel/preset-env"),
      {
        useBuiltIns: "entry",
        corejs: 3,
      },
    ],
  ],
};
```

### 选项 

- config [string]

  ​	Babel 配置文件的路径。Hugo 默认会在项目中查找 `babel.config.js` 文件。有关这些配置文件的更多信息，请参见：[babel 配置](https://babeljs.io/docs/en/configuration)。 

- minified [bool]

  Save as many bytes as possible when printing

  在打印时尽可能节省字节。  

- noComments [bool]

  将注释写入生成的输出中（默认为 true）。  

- compact [bool]

  不包括多余的空格字符和行终止符。如果未设置，默认值为`auto`。  

- verbose [bool]

  记录所有日志。  

- sourceMap [string]

  从 Babel 编译输出  `inline`  或  `external`  sourcemap。外部 sourcemap 将写入目标文件名后带有 ".map" 的目标中。输入 sourcemap 可以从 js.Build 和节点模块中读取，并合并到输出 sourcemap 中。  

### 示例

```go-html-template
{{- $transpiled := resources.Get "scripts/main.js" | babel  -}}
```

或使用选项：

```go-html-template
{{ $opts := dict "noComments" true }}
{{- $transpiled := resources.Get "scripts/main.js" | babel $opts -}}
```

## 另请参阅

- [js.Build](https://gohugo.io/hugo-pipes/js/)
- [ToCSS](https://gohugo.io/hugo-pipes/transform-to-css/)
- [highlight](https://gohugo.io/functions/highlight/)
- [Concat](https://gohugo.io/hugo-pipes/bundling/)
- [ExecuteAsTemplate](https://gohugo.io/hugo-pipes/resource-from-template/)
