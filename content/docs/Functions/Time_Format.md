+++
title = "Time_Format"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# time.Format

[https://gohugo.io/functions/dateformat/](https://gohugo.io/functions/dateformat/)

Converts a date/time to a localized string.

## 语法

```
time.Format LAYOUT INPUT
dateFormat LAYOUT INPUT
```

`time.Format` (alias `dateFormat`) converts either a `time.Time` object (e.g. `.Date`) or a timestamp string `INPUT` into the format specified by the `LAYOUT` string.

```go-html-template
{{ time.Format "Monday, Jan 2, 2006" "2015-01-21" }} → "Wednesday, Jan 21, 2015"
```

`time.Format` returns a localized string for the current language.

The `LAYOUT` string can be either:

- [Go’s Layout String](https://gohugo.io/functions/format/#gos-layout-string) to learn about how the `LAYOUT` string has to be formatted. There are also some useful examples.
- A custom Hugo layout identifier (see full list below)

See the [`time` function](https://gohugo.io/functions/time/) to convert a timestamp string to a Go `time.Time` type value.

## Date/time formatting layouts 

Go’s date layout strings can be hard to reason about, especially with multiple languages. You can alternatively use some predefined layout identifiers that will output localized dates or times:

```go-html-template
{{ .Date | time.Format ":date_long" }}
```

The full list of custom layouts with examples for English:

- `:date_full` => `Wednesday, June 6, 2018`
- `:date_long` => `June 6, 2018`
- `:date_medium` => `Jun 6, 2018`
- `:date_short` => `6/6/18`
- `:time_full` => `2:09:37 am UTC`
- `:time_long` => `2:09:37 am UTC`
- `:time_medium` => `2:09:37 am`
- `:time_short` => `2:09 am`

## 另请参阅

- [.AddDate](https://gohugo.io/functions/adddate/)
- [.Format](https://gohugo.io/functions/format/)
- [.Unix](https://gohugo.io/functions/unix/)
- [now](https://gohugo.io/functions/now/)
- [time](https://gohugo.io/functions/time/)
