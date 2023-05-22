+++
title = "Trim"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# trim

[https://gohugo.io/functions/trim/](https://gohugo.io/functions/trim/)

Returns a slice of a passed string with all leading and trailing characters from cutset removed.

## 语法

```
trim INPUT CUTSET
strings.Trim INPUT CUTSET
{{ trim "++Batman--" "+-" }} → "Batman"
```

`trim` *requires* the second argument, which tells the function specifically what to remove from the first argument. There is no default value for the second argument, so **the following usage will not work**:

```go-html-template
{{ trim .Inner }}
```

Instead, the following example tells `trim` to remove extra new lines from the content contained in the [shortcode `.Inner` variable](https://gohugo.io/variables/shortcodes/):

```go-html-template
{{ trim .Inner "\n" }}
```

Go templates also provide a simple [method for trimming whitespace](https://gohugo.io/templates/introduction/#whitespace) from either side of a Go tag by including a hyphen (`-`).

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
