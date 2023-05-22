+++
title = "Configure Markup"
weight = 6
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Configure Markup

How to handle Markdown and other markup related configuration.

## Configure Markup 

See [Goldmark](https://gohugo.io/getting-started/configuration-markup/#goldmark) for settings related to the default Markdown handler in Hugo.

Below are all markup related configuration in Hugo with their default settings:

config.

=== "yaml"

    ```yaml
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
      defaultMarkdownHandler: goldmark
      goldmark:
        extensions:
          definitionList: true
          footnote: true
          linkify: true
          linkifyProtocol: https
          strikethrough: true
          table: true
          taskList: true
          typographer: true
        parser:
          attribute:
            block: false
            title: true
          autoHeadingID: true
          autoHeadingIDType: github
          wrapStandAloneImageWithinParagraph: true
        renderer:
          hardWraps: false
          unsafe: false
          xhtml: false
      highlight:
        anchorLineNos: false
        codeFences: true
        guessSyntax: false
        hl_Lines: ""
        hl_inline: false
        lineAnchors: ""
        lineNoStart: 1
        lineNos: false
        lineNumbersInTable: true
        noClasses: true
        noHl: false
        style: monokai
        tabWidth: 4
      tableOfContents:
        endLevel: 3
        ordered: false
        startLevel: 2
    ```

=== "toml"

    ```toml
    [markup]
      defaultMarkdownHandler = 'goldmark'
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
      [markup.goldmark]
        [markup.goldmark.extensions]
          definitionList = true
          footnote = true
          linkify = true
          linkifyProtocol = 'https'
          strikethrough = true
          table = true
          taskList = true
          typographer = true
        [markup.goldmark.parser]
          autoHeadingID = true
          autoHeadingIDType = 'github'
          wrapStandAloneImageWithinParagraph = true
          [markup.goldmark.parser.attribute]
            block = false
            title = true
        [markup.goldmark.renderer]
          hardWraps = false
          unsafe = false
          xhtml = false
      [markup.highlight]
        anchorLineNos = false
        codeFences = true
        guessSyntax = false
        hl_Lines = ''
        hl_inline = false
        lineAnchors = ''
        lineNoStart = 1
        lineNos = false
        lineNumbersInTable = true
        noClasses = true
        noHl = false
        style = 'monokai'
        tabWidth = 4
      [markup.tableOfContents]
        endLevel = 3
        ordered = false
        startLevel = 2
    ```

=== "json"

    ```json
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
          },
          "defaultMarkdownHandler": "goldmark",
          "goldmark": {
             "extensions": {
                "definitionList": true,
                "footnote": true,
                "linkify": true,
                "linkifyProtocol": "https",
                "strikethrough": true,
                "table": true,
                "taskList": true,
                "typographer": true
             },
             "parser": {
                "attribute": {
                   "block": false,
                   "title": true
                },
                "autoHeadingID": true,
                "autoHeadingIDType": "github",
                "wrapStandAloneImageWithinParagraph": true
             },
             "renderer": {
                "hardWraps": false,
                "unsafe": false,
                "xhtml": false
             }
          },
          "highlight": {
             "anchorLineNos": false,
             "codeFences": true,
             "guessSyntax": false,
             "hl_Lines": "",
             "hl_inline": false,
             "lineAnchors": "",
             "lineNoStart": 1,
             "lineNos": false,
             "lineNumbersInTable": true,
             "noClasses": true,
             "noHl": false,
             "style": "monokai",
             "tabWidth": 4
          },
          "tableOfContents": {
             "endLevel": 3,
             "ordered": false,
             "startLevel": 2
          }
       }
    }
    ```



**See each section below for details.**

### Goldmark 

[Goldmark](https://github.com/yuin/goldmark/) is from Hugo 0.60 the default library used for Markdown. It’s fast, it’s [CommonMark](https://spec.commonmark.org/0.29/) compliant and it’s very flexible.

This is the default configuration:

config.

=== "yaml"

    ```yaml
    markup:
      goldmark:
        extensions:
          definitionList: true
          footnote: true
          linkify: true
          linkifyProtocol: https
          strikethrough: true
          table: true
          taskList: true
          typographer: true
        parser:
          attribute:
            block: false
            title: true
          autoHeadingID: true
          autoHeadingIDType: github
          wrapStandAloneImageWithinParagraph: true
        renderer:
          hardWraps: false
          unsafe: false
          xhtml: false
    ```

=== "toml"

    ```toml
    [markup]
      [markup.goldmark]
        [markup.goldmark.extensions]
          definitionList = true
          footnote = true
          linkify = true
          linkifyProtocol = 'https'
          strikethrough = true
          table = true
          taskList = true
          typographer = true
        [markup.goldmark.parser]
          autoHeadingID = true
          autoHeadingIDType = 'github'
          wrapStandAloneImageWithinParagraph = true
          [markup.goldmark.parser.attribute]
            block = false
            title = true
        [markup.goldmark.renderer]
          hardWraps = false
          unsafe = false
          xhtml = false
    ```

=== "json"

    ```json
    {
       "markup": {
          "goldmark": {
             "extensions": {
                "definitionList": true,
                "footnote": true,
                "linkify": true,
                "linkifyProtocol": "https",
                "strikethrough": true,
                "table": true,
                "taskList": true,
                "typographer": true
             },
             "parser": {
                "attribute": {
                   "block": false,
                   "title": true
                },
                "autoHeadingID": true,
                "autoHeadingIDType": "github",
                "wrapStandAloneImageWithinParagraph": true
             },
             "renderer": {
                "hardWraps": false,
                "unsafe": false,
                "xhtml": false
             }
          }
       }
    }
    ```



For details on the extensions, refer to [this section](https://github.com/yuin/goldmark/#built-in-extensions) of the Goldmark documentation

Some settings explained:

- hardWraps

  By default, Goldmark ignores newlines within a paragraph. Set to `true` to render newlines as `<br>` elements.

- unsafe

  By default, Goldmark does not render raw HTMLs and potentially dangerous links. If you have lots of inline HTML and/or JavaScript, you may need to turn this on.

- typographer

  This extension substitutes punctuations with typographic entities like [smartypants](https://daringfireball.net/projects/smartypants/).

- attribute

  Enable custom attribute support for titles and blocks by adding attribute lists inside single curly brackets (`{.myclass class="class1 class2" }`) and placing it *after the Markdown element it decorates*, on the same line for titles and on a new line directly below for blocks.

Hugo supports adding attributes (e.g. CSS classes) to Markdown blocks, e.g. tables, lists, paragraphs etc.

A blockquote with a CSS class:

```md
> foo
> bar
{.myclass}
```

There are some current limitations: For tables you can currently only apply it to the full table, and for lists the `ul`/`ol`-nodes only, e.g.:

```md
* Fruit
  * Apple
  * Orange
  * Banana
  {.fruits}
* Dairy
  * Milk
  * Cheese
  {.dairies}
{.list}
```

Note that attributes in [code fences](https://gohugo.io/content-management/syntax-highlighting/#highlighting-in-code-fences) must come after the opening tag, with any other highlighting processing instruction, e.g.:

~~~txt
```go {.myclass linenos=table,hl_lines=[8,"15-17"],linenostart=199}
// ... code
```
~~~

- autoHeadingIDType (“github”)

  The strategy used for creating auto IDs (anchor names). Available types are `github`, `github-ascii` and `blackfriday`. `github` produces GitHub-compatible IDs, `github-ascii` will drop any non-Ascii characters after accent normalization, and `blackfriday` will make the IDs compatible with Blackfriday, the default Markdown engine before Hugo 0.60. Note that if Goldmark is your default Markdown engine, this is also the strategy used in the [anchorize](https://gohugo.io/functions/anchorize/) template func.

### Highlight 

This is the default `highlight` configuration. Note that some of these settings can be set per code block, see [Syntax Highlighting](https://gohugo.io/content-management/syntax-highlighting/).

config.

=== "yaml"

    ```yaml
    markup:
      highlight:
        anchorLineNos: false
        codeFences: true
        guessSyntax: false
        hl_Lines: ""
        hl_inline: false
        lineAnchors: ""
        lineNoStart: 1
        lineNos: false
        lineNumbersInTable: true
        noClasses: true
        noHl: false
        style: monokai
        tabWidth: 4
    ```

=== "toml"

    ```toml
    [markup]
      [markup.highlight]
        anchorLineNos = false
        codeFences = true
        guessSyntax = false
        hl_Lines = ''
        hl_inline = false
        lineAnchors = ''
        lineNoStart = 1
        lineNos = false
        lineNumbersInTable = true
        noClasses = true
        noHl = false
        style = 'monokai'
        tabWidth = 4
    ```

=== "json"

    ```json
    {
       "markup": {
          "highlight": {
             "anchorLineNos": false,
             "codeFences": true,
             "guessSyntax": false,
             "hl_Lines": "",
             "hl_inline": false,
             "lineAnchors": "",
             "lineNoStart": 1,
             "lineNos": false,
             "lineNumbersInTable": true,
             "noClasses": true,
             "noHl": false,
             "style": "monokai",
             "tabWidth": 4
          }
       }
    }
    ```



For `style`, see these galleries:

- [Short snippets](https://xyproto.github.io/splash/docs/all.html)
- [Long snippets](https://xyproto.github.io/splash/docs/longer/all.html)

For CSS, see [Generate Syntax Highlighter CSS](https://gohugo.io/content-management/syntax-highlighting/#generate-syntax-highlighter-css).

### Table Of Contents 

config.

=== "yaml"

    ```yaml
    markup:
      tableOfContents:
        endLevel: 3
        ordered: false
        startLevel: 2
    ```

=== "toml"

    ```toml
    [markup]
      [markup.tableOfContents]
        endLevel = 3
        ordered = false
        startLevel = 2
    ```

=== "json"

    ```json
    {
       "markup": {
          "tableOfContents": {
             "endLevel": 3,
             "ordered": false,
             "startLevel": 2
          }
       }
    }
    ```



These settings only works for the Goldmark renderer:

- startLevel

  The heading level, values starting at 1 (`h1`), to start render the table of contents.

- endLevel

  The heading level, inclusive, to stop render the table of contents.

- ordered

  Whether or not to generate an ordered list instead of an unordered list.

## Markdown Render Hooks 

See [Markdown Render Hooks](https://gohugo.io/templates/render-hooks/).

## See Also

- [Configure Hugo](https://gohugo.io/getting-started/configuration/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [Syntax Highlighting](https://gohugo.io/content-management/syntax-highlighting/)
- [highlight](https://gohugo.io/functions/highlight/)
