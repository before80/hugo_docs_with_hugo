+++
title = "Lang_Merge"
weight = 60
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# lang.Merge

[https://gohugo.io/functions/lang.merge/](https://gohugo.io/functions/lang.merge/)

Merge missing translations from other languages.

## 语法

```
lang.Merge FROM TO
```

As an example:

```bash
{{ $pages := .Site.RegularPages | lang.Merge $frSite.RegularPages | lang.Merge $enSite.RegularPages }}
```

Will "fill in the gaps" in the current site with, from left to right, content from the French site, and lastly the English.

A more practical example is to fill in the missing translations from the other languages:

```bash
{{ $pages := .Site.RegularPages }}
{{ range .Site.Home.Translations }}
{{ $pages = $pages | lang.Merge .Site.RegularPages }}
{{ end }}
```

## 另请参阅

- [Multilingual Mode](https://gohugo.io/content-management/multilingual/)
- [absLangURL](https://gohugo.io/functions/abslangurl/)
- [i18n](https://gohugo.io/functions/i18n/)
- [relLangURL](https://gohugo.io/functions/rellangurl/)
- [uniq](https://gohugo.io/functions/uniq/)
