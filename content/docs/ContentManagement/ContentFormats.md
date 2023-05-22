+++
title = "内容格式"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Content Formats - 内容格式 

[https://gohugo.io/content-management/formats/](https://gohugo.io/content-management/formats/)

​	Hugo支持HTML和Markdown这两种内容格式。

​	您可以将任何文件类型放入您的 `/content` 目录下，但Hugo会使用 前置元数据 中的 `markup` 值（如果设置了）或文件扩展名（见下表中的 `Markup identifiers`）来确定是否需要处理标记语言，例如：

- Markdown 转换为 HTML 
- 处理 [Shortcodes](https://gohugo.io/content-management/shortcodes/) 
- 应用布局

## 内容格式列表 

​	Hugo当前支持的内容格式如下：

| Name           | Markup identifiers     | 备注                                                         |
| :------------- | :--------------------- | :----------------------------------------------------------- |
| Goldmark       | md, markdown, goldmark | 注意您可以将 `md` 和 `markdown` 的默认处理器设置为其他内容，请参见[配置标记](https://gohugo.io/getting-started/configuration-markup/)。 |
| Emacs Org-Mode | org                    | 参见 [go-org](https://github.com/niklasfasching/go-org).     |
| AsciiDoc       | asciidocext, adoc, ad  | 需要安装 [Asciidoctor](https://asciidoctor.org/)。           |
| RST            | rst                    | 需要安装 [RST](https://docutils.sourceforge.io/rst.html) 。  |
| Pandoc         | pandoc, pdc            | 需要安装 [Pandoc](https://www.pandoc.org/) 。                |
| HTML           | html, htm              | 要将其视为内容文件（包括布局、shortcodes等），它必须有前置元数据。否则，它将被原样复制。 |

​	`markup identifier`可以从前置元数据中的`markup`变量或文件扩展名中获取。有关标记语言相关的配置，请参见[配置标记](https://gohugo.io/getting-started/configuration-markup/)。

## 外部助手 

​	上表中的某些格式需要在您的计算机上安装外部助手。例如，对于 AsciiDoc 文件，Hugo 将尝试调用 `asciidoctor` 命令。这意味着您需要在您的计算机上安装相应的工具才能使用这些格式。

​	默认情况下，Hugo会将合理的默认参数传递给这些外部助手：

- `asciidoctor`: `--no-header-footer -`
- `rst2html`: `--leave-comments --initial-header-level=2`
- `pandoc`: `--mathjax`

> ​	由于其他格式是外部命令，生成性能将严重依赖于您正在使用的外部工具的性能。由于此功能仍处于初期阶段，因此欢迎提供反馈。

### AsciiDoc 外部助手

​	[AsciiDoc](https://github.com/asciidoc/asciidoc)实现于 2020 年 1 月结束生命周期并不再得到支持。AsciiDoc 的开发正在 [Asciidoctor](https://github.com/asciidoctor) 下继续进行。当然，AsciiDoc 格式仍然存在。但请继续使用 Asciidoctor 实现。

### Asciidoctor 外部助手

​	Asciidoctor 社区提供了一系列针对 AsciiDoc 格式的工具，可以额外安装到 Hugo 中。[请参阅 Asciidoctor 文档以获取安装说明](https://asciidoctor.org/docs/install-toolchain/)。如果需要，请确保还安装了所有可选扩展，例如 `asciidoctor-diagram` 或 `asciidoctor-html5s`。

> ​	外部 `asciidoctor` 命令要求 Hugo 将渲染内容写入磁盘的特定目标目录。必须使用命令选项 `--destination` 运行 Hugo。

​	一些 [Asciidoctor](https://asciidoctor.org/man/asciidoctor/)参数可以在 Hugo 中自定义：

| 参数             | 备注                                                         |
| :--------------- | :----------------------------------------------------------- |
| backend          | 除非您知道自己在做什么，否则不要更改此参数。                 |
| doctype          | 目前，Hugo仅支持`article`类型的文档。                        |
| extensions       | 可用的扩展包括 `asciidoctor-html5s`, `asciidoctor-bibtex`, `asciidoctor-diagram`, `asciidoctor-interdoc-reftext`, `asciidoctor-katex`, `asciidoctor-latex`, `asciidoctor-mathematical`, `asciidoctor-question`, `asciidoctor-rouge`. |
| attributes       | 用于在AsciiDoc文件中引用的变量。这是一个变量名称/值映射列表。参见[Asciidoctor的属性](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#attributes-and-substitutions)。 |
| noHeaderOrFooter | 输出一个可嵌入的文档，不包括标题、页脚和文档正文之外的内容。除非您知道自己在做什么，否则不要更改此参数。 |
| safeMode         | 安全模式级别`unsafe`、`safe`、`server`或`secure`。除非您知道自己在做什么，否则不要更改此参数。 |
| sectionNumbers   | 自动为章节标题编号。                                         |
| verbose          | 详细打印处理信息和配置文件检查到stderr。                     |
| trace            | 在错误信息中包含回溯信息。                                   |
| failureLevel     | 触发非零退出码（失败）的最小日志记录级别。                   |

​	Hugo提供了一些额外的设置，这些设置不能直接映射到Asciidoctor的CLI选项中：

- workingFolderCurrent

  将工作目录设置为正在处理的AsciiDoc文件的目录，以便[include](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#include-files)可以使用相对路径。此设置使用`asciidoctor` cli参数`--base-dir`和attribute `outdir=`. 若要使用[asciidoctor-diagram](https://asciidoctor.org/docs/asciidoctor-diagram/)渲染图表，必须将`workingFolderCurrent`设置为`true`。 

- preserveTOC

  默认情况下，Hugo会删除Asciidoctor生成的目录，并通过内置变量`.TableOfContents`提供它，以便进行进一步的自定义并更好地与各种Hugo主题集成。可以将此选项设置为`true`以保留Asciidoctor的目录。 

​	以下是所有与AsciiDoc相关的设置及其默认值：

config.

=== "yaml"

    ``` yaml
    markup:
      asciidocExt:
        attributes: {}
        backend: html5
        extensions: []
        failureLevel: fatal
        noHeaderOrFooter: true
        preserveTOC: false
        safeMode: unsafe
        sectionNumbers: false
        trace: false
        verbose: false
        workingFolderCurrent: false
    ```

=== "toml"

    ``` toml
    [markup]
      [markup.asciidocExt]
        backend = 'html5'
        extensions = []
        failureLevel = 'fatal'
        noHeaderOrFooter = true
        preserveTOC = false
        safeMode = 'unsafe'
        sectionNumbers = false
        trace = false
        verbose = false
        workingFolderCurrent = false
        [markup.asciidocExt.attributes]
    ```

=== "json"

    ``` json
    {
       "markup": {
          "asciidocExt": {
             "attributes": {},
             "backend": "html5",
             "extensions": [],
             "failureLevel": "fatal",
             "noHeaderOrFooter": true,
             "preserveTOC": false,
             "safeMode": "unsafe",
             "sectionNumbers": false,
             "trace": false,
             "verbose": false,
             "workingFolderCurrent": false
          }
       }
    }
    ```

​	请注意，出于安全考虑，只允许没有路径分隔符（`\`、`/`或`.`）的扩展名。这意味着只有在Ruby的`$LOAD_PATH`中（即，扩展名很可能是由用户安装的），扩展名才能被调用。任何相对于站点路径声明的扩展名都将不被接受。

Example of how to set extensions and attributes:

​	设置扩展名和属性的示例：

```yml
[markup.asciidocExt]
    extensions = ["asciidoctor-html5s", "asciidoctor-diagram"]
    workingFolderCurrent = true
    [markup.asciidocExt.attributes]
        my-base-url = "https://example.com/"
        my-attribute-name = "my value"
```

​	在复杂的 Asciidoctor 环境中，有时候调试带有所有参数的外部助手的确切调用是很有帮助的。使用 `-v` 选项运行 Hugo。您将得到如下输出：

```txt
INFO 2019/12/22 09:08:48 Rendering book-as-pdf.adoc with C:\Ruby26-x64\bin\asciidoctor.bat using asciidoc args [--no-header-footer -r asciidoctor-html5s -b html5s -r asciidoctor-diagram --base-dir D:\prototypes\hugo_asciidoc_ddd\docs -a outdir=D:\prototypes\hugo_asciidoc_ddd\build -] ...
```

## 学习Markdown 

​	Markdown 语法简单易学，只需花费一个短暂的时间就能掌握。以下资源是很好的起步指南：

- [Daring Fireball: Markdown, John Gruber (Creator of Markdown)](https://daringfireball.net/projects/markdown/)
- [Markdown Cheatsheet, Adam Pritchard](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [Markdown Tutorial (Interactive), Garen Torikian](https://www.markdowntutorial.com/)
- [The Markdown Guide, Matt Cone](https://www.markdownguide.org/)

## 另请参阅 

- [.RenderString](https://gohugo.io/functions/renderstring/)
- [Markdown渲染钩子 ](https://gohugo.io/templates/render-hooks/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [anchorize](https://gohugo.io/functions/anchorize/)
- [markdownify](https://gohugo.io/functions/markdownify/)
