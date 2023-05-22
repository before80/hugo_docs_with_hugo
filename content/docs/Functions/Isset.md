+++
title = "Isset"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# isset

[https://gohugo.io/functions/isset/](https://gohugo.io/functions/isset/)

Returns true if the parameter is set.

## 语法

```
isset COLLECTION INDEX
isset COLLECTION KEY
```

Takes either a slice, array, or channel and an index or a map and a key as input.

```go-html-template
{{ if isset .Params "project_url" }} {{ index .Params "project_url" }}{{ end }}
```

All site-level configuration keys are stored as lower case. Therefore, a `myParam` key-value set in your [site configuration file](https://gohugo.io/getting-started/configuration/) needs to be accessed with `{{ if isset .Site.Params "myparam" }}` and *not* with `{{ if isset .Site.Params "myParam" }}`. Note that you can still access the same config key with `.Site.Params.myParam` *or* `.Site.Params.myparam`, for example, when using [`with`](https://gohugo.io/functions/with). This restriction also applies when accessing page-level front matter keys from within [shortcodes](https://gohugo.io/content-management/shortcodes/).
