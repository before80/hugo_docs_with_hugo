+++
title = ".Scratch"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Scratch

[https://gohugo.io/functions/scratch/](https://gohugo.io/functions/scratch/)

​	该函数用作 "草稿本"，用于存储和操作数据。  

​	Scratch 是 Hugo 的一个功能，旨在方便地在 Go 模板中操纵数据。它是一个 Page 或 简码方法，其结果数据将被附加到给定的上下文中，或者它可以作为存储在变量中的唯一实例。  

​	请注意，Scratch 最初是作为一个解决方案创建的，以解决影响 0.48 版本之前的 Hugo 的[Go 模板作用域限制问题](https://github.com/golang/go/issues/10608)。有关`.Scratch`和上下文用例的详细分析，请参阅[这篇博客文章](https://regisphilibert.com/blog/2017/04/hugo-scratch-explained-variable/)。

### 带有上下文的  `.Scratch`  vs. 本地的  `newScratch`  

​	自 Hugo 0.43 起，有两种使用 Scratch 的不同方式：  

#### 页面的 .Scratch 

  `.Scratch`  作为Page 方法或 简码方法可用，并将“草稿”数据附加到给定页面上。使用  `.Scratch`  必须要在 Page 或 简码上下文中。

```go-html-template
{{ .Scratch.Set "greeting" "bonjour" }}
{{ range .Pages }}
  {{ .Scratch.Set "greeting" (print "bonjour" .Title) }}
{{ end }}
```

#### 本地的  `newScratch`  

​	使用  `newScratch`  函数，可以将 Scratch 实例分配给任何变量。 在这种情况下，不需要Page 或 简码上下文，而 Scratch 的作用域仅为本地。以下方法可以从已分配 Scratch 实例的变量中使用：

```go-html-template
{{ $data := newScratch }}
{{ $data.Set "greeting" "hola" }}
```

### 方法

​	Scratch 具有以下方法：  

​	请注意，以下示例假设已在  `$scratch`  中存储了 [本地 Scratch 实例](https://gohugo.io/functions/scratch/#the-local-newscratch)。 

#### .Set 

​	设置给定键的值。

```go-html-template
{{ $scratch.Set "greeting" "Hello" }}
```

#### .Get 

​	获取给定键的值。

```go-html-template
{{ $scratch.Set "greeting" "Hello" }}
----
{{ $scratch.Get "greeting" }} > Hello
```

#### .Add 

​	将给定值添加到给定键的现有值中。  

​	对于单个值，`Add`接受支持 Go 的 `+` 运算符的值。如果某个键的第一个 `Add` 是一个数组或切片，则后续添加的内容将追加到该列表中。

```go-html-template
{{ $scratch.Add "greetings" "Hello" }}
{{ $scratch.Add "greetings" "Welcome" }}
----
{{ $scratch.Get "greetings" }} > HelloWelcome
{{ $scratch.Add "total" 3 }}
{{ $scratch.Add "total" 7 }}
----
{{ $scratch.Get "total" }} > 10
{{ $scratch.Add "greetings" (slice "Hello") }}
{{ $scratch.Add "greetings" (slice "Welcome" "Cheers") }}
----
{{ $scratch.Get "greetings" }} > []interface {}{"Hello", "Welcome", "Cheers"}
```

#### .SetInMap 

Takes a `key`, `mapKey` and `value` and adds a map of `mapKey` and `value` to the given `key`.

​	接收一个 `key` 、 `mapKey` 和 `value` ，并将 `mapKey` 和 `value` 的映射添加到给定的 `key` 中。

```go-html-template
{{ $scratch.SetInMap "greetings" "english" "Hello" }}
{{ $scratch.SetInMap "greetings" "french" "Bonjour" }}
----
{{ $scratch.Get "greetings" }} > map[french:Bonjour english:Hello]
```

#### .DeleteInMap 

Takes a `key` and `mapKey` and removes the map of `mapKey` from the given `key`.

​	接收一个 `key` 和 `mapKey` ，并从给定的 `key` 中删除 `mapKey` 的映射。

```go-html-template
{{ .Scratch.SetInMap "greetings" "english" "Hello" }}
{{ .Scratch.SetInMap "greetings" "french" "Bonjour" }}
----
{{ .Scratch.DeleteInMap "greetings" "english" }}
----
{{ .Scratch.Get "greetings" }} > map[french:Bonjour]
```

#### .GetSortedMapValues 

Return an array of values from `key` sorted by `mapKey`.

​	按 `mapKey` 排序，返回 `key` 中的值数组。

```go-html-template
{{ $scratch.SetInMap "greetings" "english" "Hello" }}
{{ $scratch.SetInMap "greetings" "french" "Bonjour" }}
----
{{ $scratch.GetSortedMapValues "greetings" }} > [Hello Bonjour]
```

#### .Delete 

Remove the given key.

​	删除给定的键。

```go-html-template
{{ $scratch.Set "greeting" "Hello" }}
----
{{ $scratch.Delete "greeting" }}
```

#### .Values 

Return the raw backing map. Note that you should only use this method on the locally scoped Scratch instances you obtain via [`newScratch`](https://gohugo.io/functions/scratch/#the-local-newscratch), not `.Page.Scratch` etc., as that will lead to concurrency issues.

​	返回原始的后备映射。注意，只应在通过[ `newScratch` ](https://gohugo.io/functions/scratch/#the-local-newscratch)获得的局部范围的Scratch实例上使用此方法，而不是 `.Page.Scratch` 等，因为会导致并发问题。  

## 另请参阅

- [.Store](https://gohugo.io/functions/store/)
- [Menu Variables](https://gohugo.io/variables/menus/)
- [Page Resources](https://gohugo.io/content-management/page-resources/)
- [after](https://gohugo.io/functions/after/)
- [delimit](https://gohugo.io/functions/delimit/)
