+++
title = "FindRE"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# findRE

[https://gohugo.io/functions/findre/](https://gohugo.io/functions/findre/)

Returns a slice of strings that match the regular expression.

## 语法

```
findRE PATTERN INPUT [LIMIT]
strings.FindRE PATTERN INPUT [LIMIT]
```

By default, `findRE` finds all matches. You can limit the number of matches with an optional LIMIT parameter.

When specifying the regular expression, use a raw [string literal](https://go.dev/ref/spec#String_literals) (backticks) instead of an interpreted string literal (double quotes) to simplify the syntax. With an interpreted string literal you must escape backslashes.

This function uses the [RE2](https://github.com/google/re2/) regular expression library. See the [RE2 syntax documentation](https://github.com/google/re2/wiki/Syntax/) for details. Note that the RE2 `\C` escape sequence is not supported.

The RE2 syntax is a subset of that accepted by [PCRE](https://www.pcre.org/), roughly speaking, and with various [caveats](https://swtch.com/~rsc/regexp/regexp3.html#caveats).

This example returns a slice of all second level headings (`h2` elements) within the rendered `.Content`:

```go-html-template
{{ findRE `(?s)<h2.*?>.*?</h2>` .Content }}
```

The `s` flag causes `.` to match `\n` as well, allowing us to find an `h2` element that contains newlines.

To limit the number of matches to one:

```go-html-template
{{ findRE `(?s)<h2.*?>.*?</h2>` .Content 1 }}
```

You can write and test your regular expression using [regex101.com](https://regex101.com/). Be sure to select the Go flavor before you begin.

## 另请参阅

- [findRESubmatch](https://gohugo.io/functions/findresubmatch/)
- [replaceRE](https://gohugo.io/functions/replacere/)
