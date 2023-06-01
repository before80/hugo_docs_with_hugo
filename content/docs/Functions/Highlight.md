+++
title = "highlight"
weight = 45
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# highlight

[https://gohugo.io/functions/highlight/](https://gohugo.io/functions/highlight/)

Renders code with a syntax highlighter.

## 语法

```
transform.Highlight INPUT LANG [OPTIONS]
highlight INPUT LANG [OPTIONS]
```

The `highlight` function uses the [Chroma](https://github.com/alecthomas/chroma) syntax highlighter, supporting over 200 languages with more than 40 available styles.

## Parameters 

- INPUT

  The code to highlight.

- LANG

  The language of the code to highlight. Choose from one of the [supported languages](https://gohugo.io/content-management/syntax-highlighting#list-of-chroma-highlighting-languages). Case-insensitive.

- OPTIONS

  An optional, comma-separated list of zero or more [options](https://gohugo.io/functions/highlight/#options). Set default values in [site configuration](https://gohugo.io/getting-started/configuration-markup#highlight).

## Options 

- lineNos

  Boolean. Default is `false`. Display a number at the beginning of each line.

- lineNumbersInTable

  Boolean. Default is `true`. Render the highlighted code in an HTML table with two cells. The left table cell contains the line numbers. The right table cell contains the code, allowing a user to select and copy the code without line numbers. Irrelevant if `lineNos` is `false`.

- anchorLineNos

  Boolean. Default is `false`. Render each line number as an HTML anchor element, and set the `id` attribute of the surrounding `<span>` to the line number. Irrelevant if `lineNos` is `false`.

- lineAnchors

  String. Default is `""`. When rendering a line number as an HTML anchor element, prepend this value to the `id` attribute of the surrounding `<span>`. This provides unique `id` attributes when a page contains two or more code blocks. Irrelevant if `lineNos` or `anchorLineNos` is `false`.

- lineNoStart

  Integer. Default is `1`. The number to display at the beginning of the first line. Irrelevant if `lineNos` is `false`.

- hl_Lines

  String. Default is `""`. A space-separated list of lines to emphasize within the highlighted code. To emphasize lines 2, 3, 4, and 7, set this value to `2-4 7`. This option is independent of the `lineNoStart` option.

- hl_inline

  Boolean. Default is `false`. Render the highlighted code without a wrapping container.

- style

  String. Default is `monokai`. The CSS styles to apply to the highlighted code. See the [style gallery](https://xyproto.github.io/splash/docs/) for examples. Case-sensitive.

- noClasses

  Boolean. Default is `true`. Use inline CSS styles instead of an external CSS file. To use an external CSS file, set this value to `false` and [generate the file with the hugo client](https://gohugo.io/commands/hugo_gen_chromastyles).

- tabWidth

  Integer. Default is `4`. Substitute this number of spaces for each tab character in your highlighted code. Irrelevant if `noClasses` is `false`.

- guessSyntax

  Boolean. Default is `false`. If the `LANG` parameter is blank or an unrecognized language, auto-detect the language if possible, otherwise use a fallback language.

Instead of specifying both `lineNos` and `lineNumbersInTable`, you can use the following shorthand notation:

- `lineNos=inline`

  equivalent to `lineNos=true` and `lineNumbersInTable=false`

- `lineNos=table`

  equivalent to `lineNos=true` and `lineNumbersInTable=true`

## Examples 

```go-html-template
{{ $input := `fmt.Println("Hello World!")` }}
{{ transform.Highlight $input "go" }}

{{ $input := `console.log('Hello World!');` }}
{{ $lang := "js" }}
{{ transform.Highlight $input $lang "lineNos=table, style=api" }}

{{ $input := `echo "Hello World!"` }}
{{ $lang := "bash" }}
{{ $options := slice "lineNos=table" "style=dracula" }}
{{ transform.Highlight $input $lang (delimit $options ",") }}
```

## 另请参阅

- [Syntax Highlighting](https://gohugo.io/content-management/syntax-highlighting/)
- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [js.Build](https://gohugo.io/hugo-pipes/js/)
- [Configure Markup](https://gohugo.io/getting-started/configuration-markup/)
- [File Variables](https://gohugo.io/variables/files/)
