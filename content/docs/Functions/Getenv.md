+++
title = "Getenv"
weight = 42
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# getenv

[https://gohugo.io/functions/getenv/](https://gohugo.io/functions/getenv/)

Returns the value of an environment variable, or an empty string if the environment variable is not set.

## 语法

```
os.Getenv VARIABLE
getenv VARIABLE
```

Examples:

```go-html-template
{{ os.Getenv "HOME" }} --> /home/victor
{{ os.Getenv "USER" }} --> victor
```

You can pass values when building your site:

```bash
MY_VAR1=foo MY_VAR2=bar hugo

OR

export MY_VAR1=foo
export MY_VAR2=bar
hugo
```

And then retrieve the values within a template:

```go-html-template
{{ os.Getenv "MY_VAR1" }} --> foo
{{ os.Getenv "MY_VAR2" }} --> bar
```

With Hugo v0.91.0 and later, you must explicitly allow access to environment variables. For details, review [Hugo’s Security Policy](https://gohugo.io/about/security-model/#security-policy). By default, environment variables beginning with `HUGO_` are allowed when using the `os.Getenv` function.
