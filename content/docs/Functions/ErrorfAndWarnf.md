+++
title = "errorf 和 warnf"
weight = 34
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# errorf and warnf

[https://gohugo.io/functions/errorf/](https://gohugo.io/functions/errorf/)

Log ERROR or WARNING from the templates.

## 语法

```
errorf FORMAT INPUT
```

`errorf` or `warnf` will evaluate a format string, then output the result to the ERROR or WARNING log (and only once per error message to avoid flooding the log).

Any ERROR will also cause the build to fail (the `hugo` command will `exit -1`).

Both functions return an empty string, so the messages are only printed to the console.

```go-html-template
{{ errorf "Failed to handle page %q" .Path }}
{{ warnf "You should update the shortcodes in %q" .Path }}
```

Note that `errorf`, `erroridf`, and `warnf` support all the formatting verbs of the [fmt](https://pkg.go.dev/fmt) package.

## Suppress errors 

Sometimes it may make sense to let the user suppress an ERROR and make the build succeed.

You can do this by using the `erroridf` function. This functions takes an error ID as the first argument.

```go-html-template
{{ erroridf "my-custom-error" "You should consider fixing this." }}
```

This will produce:

```
ERROR 2021/06/07 17:47:38 You should consider fixing this.
If you feel that this should not be logged as an ERROR, you can ignore it by adding this to your site config:
ignoreErrors = ["my-custom-error"]
```

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
- [humanize](https://gohugo.io/functions/humanize/)
