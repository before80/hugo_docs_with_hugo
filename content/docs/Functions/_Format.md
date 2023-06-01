+++
title = ".Format"
weight = 2
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Format

[https://gohugo.io/functions/format/](https://gohugo.io/functions/format/)

​	根据 Go 的布局字符串格式化内置的 Hugo 日期 ——  `.Date` ， `.PublishDate`  和  `.Lastmod` 。  

## 语法

```
.Format FORMAT
```

​	`.Format` 将格式化在前置元数据中定义的日期值，并可用作以下[页面变量](https://gohugo.io/variables/page/)的属性: 

- `.PublishDate`
- `.Date`
- `.Lastmod`

​	假设内容文件前置元数据中有一个键值对  `date: 2017-03-03` ，可以通过  `.Format` ，后跟期望输出的布局字符串来将日期处理后再构建：

```go-html-template
{{ .PublishDate.Format "January 2, 2006" }} => March 3, 2017
```

​	要格式化您前置元数据中定义的*任何*日期字符串表示形式，请参见[ `dateFormat`  函数](https://gohugo.io/functions/dateformat/)，它仍将利用下面解释的Go 布局字符串，但使用略有不同的语法。  

## Go 的布局字符串

​	模板通过布局字符串[格式化您的日期](https://golang.org/pkg/time/)，该字符串指向特定的参考时间：

```
Mon Jan 2 15:04:05 MST 2006
```

​	虽然这可能看起来是任意的，但  `MST`  的数字值为  `07` ，因此使布局字符串成为数字序列。  

​	这里有一个可视化解释[直接取自 Go 文档](https://golang.org/pkg/time/#example_Time_Format)：

```
 Jan 2 15:04:05 2006 MST
=> 1 2  3  4  5    6  -7
```

### Hugo 日期和时间模板参考 

​	以下示例显示布局字符串，后跟渲染的输出。  

​	这些示例在[CST](https://en.wikipedia.org/wiki/Central_Time_Zone)中进行了渲染和测试，并且都指向内容文件前置元数据中的同一字段：

```
date: 2017-03-03T14:15:59-06:00
```

- `.Date` (即通过[页面变量](https://gohugo.io/variables/page/)进行调用)

  **返回**：`2017-03-03 14:15:59 -0600 CST`

- `"Monday, January 2, 2006"`

  **返回**：`Friday, March 3, 2017`

- `"Mon Jan 2 2006"`

  **返回**：`Fri Mar 3 2017`

- `"January 2006"`

  **返回**：`March 2017`

- `"2006-01-02"`

  **返回**：`2017-03-03`

- `"Monday"`

  **返回**：`Friday`

- `"02 Jan 06 15:04 MST"` (RFC822)

  **返回**：`03 Mar 17 14:15 CST`

- `"02 Jan 06 15:04 -0700"` (RFC822Z)

  **返回**：`03 Mar 17 14:15 -0600`

- `"Mon, 02 Jan 2006 15:04:05 MST"` (RFC1123)

  **返回**：`Fri, 03 Mar 2017 14:15:59 CST`

- `"Mon, 02 Jan 2006 15:04:05 -0700"` (RFC1123Z)

  **返回**：`Fri, 03 Mar 2017 14:15:59 -0600`

​	有关更多示例，请参见[go文档中的time包](https://golang.org/pkg/time/#ANSIC)。 

### 基数和序数缩写

​	目前不支持拼写出的基数（例如"one"，"two"和"three"）。  

​	使用[ humanize](https://gohugo.io/functions/humanize)函数将月份的日期渲染为序数：

```go-html-template
{{ humanize .Date.Day }} of {{ .Date.Format "January 2006" }}
```

​	这将输出：

```
5th of March 2017
```

###  使用 `.Local` 和`.UTC` 

​	与[ `dateFormat`  函数](https://gohugo.io/functions/dateformat/)一起使用，您还可以将日期转换为 `UTC` 或本地时区：  

- `{{ dateFormat "02 Jan 06 15:04 MST" .Date.UTC }}`

  **返回**：`03 Mar 17 20:15 UTC`

- `{{ dateFormat "02 Jan 06 15:04 MST" .Date.Local }}`

  **返回**：`03 Mar 17 14:15 CST`

## 另请参阅

- [.AddDate](https://gohugo.io/functions/adddate/)
- [.Unix](https://gohugo.io/functions/unix/)
- [now](https://gohugo.io/functions/now/)
- [time](https://gohugo.io/functions/time/)
- [time.Format](https://gohugo.io/functions/dateformat/)
