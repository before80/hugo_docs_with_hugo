+++
title = "lang"
weight = 59
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
## [ ](https://gohugo.io/functions/lang/#langformataccounting)lang.FormatAccounting

[https://gohugo.io/functions/lang/](https://gohugo.io/functions/lang/)

FormatAccounting returns the currency representation of number for the given currency and precision for the current language in accounting notation.

The return value is formatted with at least two decimal places.



#### 语法

lang.FormatAccounting PRECISION, CURRENCY, NUMBER

#### Examples

```go-html-template
{{ 512.5032 | lang.FormatAccounting 2 "NOK" }} ---> NOK512.50
```

## [ ](https://gohugo.io/functions/lang/#langformatcurrency)lang.FormatCurrency



FormatCurrency returns the currency representation of number for the given currency and precision for the current language.

The return value is formatted with at least two decimal places.



#### 语法

lang.FormatCurrency PRECISION, CURRENCY, NUMBER

#### Examples

```go-html-template
{{ 512.5032 | lang.FormatCurrency 2 "USD" }} ---> $512.50
```

## [ ](https://gohugo.io/functions/lang/#langformatnumber)lang.FormatNumber

FormatNumber formats number with the given precision for the current language.

#### 语法

lang.FormatNumber PRECISION, NUMBER

#### Examples

```go-html-template
{{ 512.5032 | lang.FormatNumber 2 }} ---> 512.50
```

## [ ](https://gohugo.io/functions/lang/#langformatnumbercustom)lang.FormatNumberCustom



FormatNumberCustom formats a number with the given precision using the negative, decimal, and grouping options. The `options` parameter is a string consisting of `<negative> <decimal> <grouping>`. The default `options` value is `- . ,`.

Note that numbers are rounded up at 5 or greater. So, with precision set to 0, 1.5 becomes `2`, and 1.4 becomes `1`.

For a simpler function that adapts to the current language, see FormatNumber.



#### 语法

lang.FormatNumberCustom PRECISION, NUMBER, OPTIONS

#### Examples

```go-html-template
{{ lang.FormatNumberCustom 2 12345.6789 }} ---> 12,345.68
{{ lang.FormatNumberCustom 2 12345.6789 "- , ." }} ---> 12.345,68
{{ lang.FormatNumberCustom 6 -12345.6789 "- ." }} ---> -12345.678900
{{ lang.FormatNumberCustom 0 -12345.6789 "- . ," }} ---> -12,346
{{ -98765.4321 | lang.FormatNumberCustom 2 }} ---> -98,765.43
```

## [ ](https://gohugo.io/functions/lang/#langformatpercent)lang.FormatPercent

FormatPercent formats number with the given precision for the current language. Note that the number is assumed to be a percentage.

#### 语法

lang.FormatPercent PRECISION, NUMBER

#### Examples

```go-html-template
{{ 512.5032 | lang.FormatPercent 2 }} ---> 512.50%
```

## [ ](https://gohugo.io/functions/lang/#langtranslate)lang.Translate

Translate returns a translated string for id.

#### 语法

lang.Translate ID, ARGS

#### Aliases

i18n, T
