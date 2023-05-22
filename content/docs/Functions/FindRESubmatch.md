+++
title = "FindRESubmatch"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# ndRESubmatch

[https://gohugo.io/functions/findresubmatch/](https://gohugo.io/functions/findresubmatch/)

Returns a slice of all successive matches of the regular expression. Each element is a slice of strings holding the text of the leftmost match of the regular expression and the matches, if any, of its subexpressions.

## 语法

```
findRESubmatch PATTERN INPUT [LIMIT]
strings.FindRESubmatch PATTERN INPUT [LIMIT]
```

By default, `findRESubmatch` finds all matches. You can limit the number of matches with an optional LIMIT parameter. A return value of nil indicates no match.

When specifying the regular expression, use a raw [string literal](https://go.dev/ref/spec#String_literals) (backticks) instead of an interpreted string literal (double quotes) to simplify the syntax. With an interpreted string literal you must escape backslashes.

This function uses the [RE2](https://github.com/google/re2/) regular expression library. See the [RE2 syntax documentation](https://github.com/google/re2/wiki/Syntax/) for details. Note that the RE2 `\C` escape sequence is not supported.

The RE2 syntax is a subset of that accepted by [PCRE](https://www.pcre.org/), roughly speaking, and with various [caveats](https://swtch.com/~rsc/regexp/regexp3.html#caveats).

## Demonstrative examples 

```go-html-template
{{ findRESubmatch `a(x*)b` "-ab-" }} → [["ab" ""]]
{{ findRESubmatch `a(x*)b` "-axxb-" }} → [["axxb" "xx"]]
{{ findRESubmatch `a(x*)b` "-ab-axb-" }} → [["ab" ""] ["axb" "x"]]
{{ findRESubmatch `a(x*)b` "-axxb-ab-" }} → [["axxb" "xx"] ["ab" ""]]
{{ findRESubmatch `a(x*)b` "-axxb-ab-" 1 }} → [["axxb" "xx"]]
```

## Practical example 

This markdown:

```text
- [Example](https://example.org)
- [Hugo](https://gohugo.io)
```

Produces this HTML:

```html
<ul>
  <li><a href="https://example.org">Example</a></li>
  <li><a href="https://gohugo.io">Hugo</a></li>
</ul>
```

To match the anchor elements, capturing the link destination and text:

```go-html-template
{{ $regex := `<a\s*href="(.+?)">(.+?)</a>` }}
{{ $matches := findRESubmatch $regex .Content }}
```

Viewed as JSON, the data structure of `$matches` in the code above is:

```json
[
  [
    "<a href=\"https://example.org\"></a>Example</a>",
    "https://example.org",
    "Example"
  ],
  [
    "<a href=\"https://gohugo.io\">Hugo</a>",
    "https://gohugo.io",
    "Hugo"
  ]
]
```

To render the `href` attributes:

```go-html-template
{{ range $matches }}
  {{ index . 1 }}
{{ end }}
```

Result:

```text
https://example.org
https://gohugo.io
```

You can write and test your regular expression using [regex101.com](https://regex101.com/). Be sure to select the Go flavor before you begin.

## 另请参阅

- [findRE](https://gohugo.io/functions/findre/)
- [replaceRE](https://gohugo.io/functions/replacere/)
