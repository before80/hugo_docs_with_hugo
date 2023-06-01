+++
title = ".AddDate"
weight = 1
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# .AddDate

​	返回将给定的年数、月数和天数添加到给定的 time.Time 值所得到的时间。

## 语法

```
.AddDate YEARS MONTHS DAYS
{{ $d := "2022-01-01" | time.AsTime }}

{{ $d.AddDate 0 0 1 | time.Format "2006-01-02" }} --> 2022-01-02
{{ $d.AddDate 0 1 1 | time.Format "2006-01-02" }} --> 2022-02-02
{{ $d.AddDate 1 1 1 | time.Format "2006-01-02" }} --> 2023-02-02

{{ $d.AddDate -1 -1 -1 | time.Format "2006-01-02" }} --> 2020-11-30
```

​	当增加月份或年份时，如果所得日期不存在，Hugo会将最终的  `time.Time`  值规范化。例如，在1月31日后增加一个月，会得到3月2日或3月3日，具体取决于年份。  

​	参见Go团队的[解释](https://github.com/golang/go/issues/31145#issuecomment-479067967)。

```go-html-template
{{ $d := "2023-01-31" | time.AsTime }}
{{ $d.AddDate 0 1 0 | time.Format "2006-01-02" }} --> 2023-03-03

{{ $d := "2024-01-31" | time.AsTime }}
{{ $d.AddDate 0 1 0 | time.Format "2006-01-02" }} --> 2024-03-02

{{ $d := "2024-02-29" | time.AsTime }}
{{ $d.AddDate 1 0 0 | time.Format "2006-01-02" }} --> 2025-03-01
```

## 另请参阅

- [.Format](https://gohugo.io/functions/format/)
- [.Unix](https://gohugo.io/functions/unix/)
- [now](https://gohugo.io/functions/now/)
- [time](https://gohugo.io/functions/time/)
- [time.Format](https://gohugo.io/functions/dateformat/)
