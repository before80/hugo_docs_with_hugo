+++
title = "time"
weight = 128
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# time

[https://gohugo.io/functions/time/](https://gohugo.io/functions/time/)

Converts a timestamp string into a `time.Time` structure.

## 语法

```
time INPUT [TIMEZONE]
```

`time` converts a timestamp string with an optional default location into a [`time.Time`](https://godoc.org/time#Time) structure so you can access its fields:

```go-html-template
{{ time "2016-05-28" }} → "2016-05-28T00:00:00Z"
{{ (time "2016-05-28").YearDay }} → 149
{{ mul 1000 (time "2016-05-28T10:30:00.00+10:00").Unix }} → 1464395400000, or Unix time in milliseconds
```

## Using Locations 

The optional `TIMEZONE` parameter is a string that sets a default time zone (or more specific, the location, which represents the collection of time offsets in a geographical area) that is associated with the specified time value. If the time value has an explicit timezone or offset specified, it will take precedence over the `TIMEZONE` parameter.

The list of valid locations may be system dependent, but should include `UTC`, `Local`, or any location in the [IANA Time Zone database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

If no `TIMEZONE` is set, the `timeZone` from site configuration will be used.

```go-html-template
{{ time "2020-10-20" }} → 2020-10-20 00:00:00 +0000 UTC
{{ time "2020-10-20" "America/Los_Angeles" }} → 2020-10-20 00:00:00 -0700 PDT
{{ time "2020-01-20" "America/Los_Angeles" }} → 2020-01-20 00:00:00 -0800 PST
```

## Example: Using `time` to get Month Index 

The following example takes a UNIX timestamp—set as `utimestamp: "1489276800"` in a content’s front matter—converts the timestamp (string) to an integer using the [`int` function](https://gohugo.io/functions/int/), and then uses [`printf`](https://gohugo.io/functions/printf/) to convert the `Month` property of `time` into an index.

The following example may be useful when setting up [multilingual sites](https://gohugo.io/content-management/multilingual/):

unix-to-month-integer.html



```go-html-template
{{ $time := time (int .Params.addDate)}}
=> $time = 1489276800
{{ $time.Month }}
=> "March"
{{ $monthindex := printf "%d" $time.Month }}
=> $monthindex = 3
```

## 另请参阅

- [.AddDate](https://gohugo.io/functions/adddate/)
- [.Format](https://gohugo.io/functions/format/)
- [.Unix](https://gohugo.io/functions/unix/)
- [now](https://gohugo.io/functions/now/)
- [time.Format](https://gohugo.io/functions/dateformat/)
