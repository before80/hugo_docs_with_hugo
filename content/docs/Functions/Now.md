+++
title = "Now"
weight = 71
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# now

[https://gohugo.io/functions/now/](https://gohugo.io/functions/now/)

Returns the current local time

## 语法

```
now
```

See [`time.Time`](https://godoc.org/time#Time).

For example, building your site on June 24, 2017, with the following templating:

```go-html-template
<div>
    <small>&copy; {{ now.Format "2006" }}</small>
</div>
```

would produce the following:

```html
<div>
    <small>&copy; 2017</small>
</div>
```

The above example uses the [`.Format` function](https://gohugo.io/functions/format), which page includes a full listing of date formatting using Go’s layout string.

Older Hugo themes may still be using the obsolete Page’s `.Now` (uppercase with leading dot), which causes build error that looks like the following:

```
ERROR ... Error while rendering "..." in "...": ...
executing "..." at <.Now.Format>:
can't evaluate field Now in type *hugolib.PageOutput
```

Be sure to use `now` (lowercase with ***no*** leading dot) in your templating.

## 另请参阅

- [.AddDate](https://gohugo.io/functions/adddate/)
- [.Format](https://gohugo.io/functions/format/)
- [.Unix](https://gohugo.io/functions/unix/)
- [time](https://gohugo.io/functions/time/)
- [time.Format](https://gohugo.io/functions/dateformat/)
