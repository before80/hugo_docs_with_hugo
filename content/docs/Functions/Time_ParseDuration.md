+++
title = "Time_ParseDuration"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# time.ParseDuration

[https://gohugo.io/functions/time.parseduration/](https://gohugo.io/functions/time.parseduration/)

Parses a given duration string into a `time.Duration` structure.

## 语法

```
time.ParseDuration DURATION
```

`time.ParseDuration` parses a duration string into a [`time.Duration`](https://pkg.go.dev/time#Duration) structure so you can access its fields. A duration string is a possibly signed sequence of decimal numbers, each with optional fraction and a unit suffix, such as `300ms`, `-1.5h` or `2h45m`. Valid time units are `ns`, `us` (or `µs`), `ms`, `s`, `m`, `h`.

You can perform [time operations](https://pkg.go.dev/time#Duration) on the returned `time.Duration` value:

```
{{ printf "There are %.0f seconds in one day." (time.ParseDuration "24h").Seconds }}
<!-- Output: There are 86400 seconds in one day. -->
```
