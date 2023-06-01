+++
title = "ReplaceRE"
weight = 97
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# replaceRE

[https://gohugo.io/functions/replacere/](https://gohugo.io/functions/replacere/)

Returns a string, replacing all occurrences of a regular expression with a replacement pattern.

## 语法

```
replaceRE PATTERN REPLACEMENT INPUT [LIMIT]
strings.ReplaceRE PATTERN REPLACEMENT INPUT [LIMIT]
```

By default, `replaceRE` replaces all matches. You can limit the number of matches with an optional LIMIT parameter.

When specifying the regular expression, use a raw [string literal](https://go.dev/ref/spec#String_literals) (backticks) instead of an interpreted string literal (double quotes) to simplify the syntax. With an interpreted string literal you must escape backslashes.

This function uses the [RE2](https://github.com/google/re2/) regular expression library. See the [RE2 syntax documentation](https://github.com/google/re2/wiki/Syntax/) for details. Note that the RE2 `\C` escape sequence is not supported.

The RE2 syntax is a subset of that accepted by [PCRE](https://www.pcre.org/), roughly speaking, and with various [caveats](https://swtch.com/~rsc/regexp/regexp3.html#caveats).

This example replaces two or more consecutive hyphens with a single hyphen:

```go-html-template
{{ $s := "a-b--c---d" }}
{{ replaceRE `(-{2,})` "-" $s }} → a-b-c-d
```

To limit the number of replacements to one:

```go-html-template
{{ $s := "a-b--c---d" }}
{{ replaceRE `(-{2,})` "-" $s 1 }} → a-b-c---d
```

You can use `$1`, `$2`, etc. within the replacement string to insert the groups captured within the regular expression:

```go-html-template
{{ $s := "http://gohugo.io/docs" }}
{{ replaceRE "^https?://([^/]+).*" "$1" $s }} → gohugo.io
```

You can write and test your regular expression using [regex101.com](https://regex101.com/). Be sure to select the Go flavor before you begin.

## 另请参阅

- [findRE](https://gohugo.io/functions/findre/)
- [findRESubmatch](https://gohugo.io/functions/findresubmatch/)
