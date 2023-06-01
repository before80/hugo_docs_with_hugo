+++
title = "title"
weight = 131
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# title

[https://gohugo.io/functions/title/](https://gohugo.io/functions/title/)

​	将提供的字符串转换为标题大小写样式。  

## 语法

```
title STRING
strings.Title STRING
{{ title "table of contents (TOC)" }} → "Table of Contents (TOC)"
```

​	默认情况下，Hugo 遵循[美联社风格指南（Associated Press (AP) Stylebook）](https://www.apstylebook.com/)的大写规则。如果您更喜欢遵循[芝加哥手册风格（Chicago Manual of Style）](https://www.chicagomanualofstyle.org/home.html)，或者使用 Go 的惯例将每个单词都大写，请更改您的[站点配置](https://gohugo.io/getting-started/configuration/#configure-title-case)。

## 另请参阅

- [anchorize](https://gohugo.io/functions/anchorize/)
- [emojify](https://gohugo.io/functions/emojify/)
- [errorf and warnf](https://gohugo.io/functions/errorf/)
- [float](https://gohugo.io/functions/float/)
- [htmlEscape](https://gohugo.io/functions/htmlescape/)
