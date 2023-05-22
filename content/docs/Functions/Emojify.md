+++
title = "Emojify"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# emojify

[https://gohugo.io/functions/emojify/](https://gohugo.io/functions/emojify/)

Runs a string through the Emoji emoticons processor.

## 语法

```
emojify INPUT
```

`emojify` runs a passed string through the Emoji emoticons processor.

See the [Emoji cheat sheet](https://www.webfx.com/tools/emoji-cheat-sheet/) for available emoticons.

The `emojify` function can be called in your templates but not directly in your content files by default. For emojis in content files, set `enableEmoji` to `true` in your site’s [configuration](https://gohugo.io/getting-started/configuration/). Then you can write emoji shorthand directly into your content files; e.g. I :heart: Hugo!:

I ❤️ Hugo!

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
- [humanize](https://gohugo.io/functions/humanize/)
