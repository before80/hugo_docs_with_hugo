+++
title = ".Unix"
weight = 13
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Unix

[https://gohugo.io/functions/unix/](https://gohugo.io/functions/unix/)

Converts a time.Time value to the number of seconds elapsed since the Unix epoch, excluding leap seconds. The Unix epoch is 00:00:00 UTC on 1 January 1970.

## 语法

```
.Unix
.UnixMilli
.UnixMicro
.UnixNano
```

The `Milli`, `Micro`, and `Nano` variants return the number of milliseconds, microseconds, and nanoseconds (respectively) elapsed since the Unix epoch.

```go-html-template
.Date.Unix        --> 1637259694
.ExpiryDate.Unix  --> 1672559999
.Lastmod.Unix     --> 1637361786
.PublishDate.Unix --> 1637421261

("1970-01-01T00:00:00-00:00" | time.AsTime).Unix --> 0
("1970-01-01T00:00:42-00:00" | time.AsTime).Unix --> 42
("1970-04-11T01:48:29-08:00" | time.AsTime).Unix --> 8675309
("2026-05-02T20:09:31-07:00" | time.AsTime).Unix --> 1777777771

now.Unix      --> 1637447841
now.UnixMilli --> 1637447841347
now.UnixMicro --> 1637447841347378
now.UnixNano  --> 1637447841347378799
```

## 另请参阅

- [.AddDate](https://gohugo.io/functions/adddate/)
- [.Format](https://gohugo.io/functions/format/)
- [now](https://gohugo.io/functions/now/)
- [time](https://gohugo.io/functions/time/)
- [time.Format](https://gohugo.io/functions/dateformat/)
