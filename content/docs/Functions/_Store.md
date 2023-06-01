+++
title = ".Store"
weight = 12
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .Store

[https://gohugo.io/functions/store/](https://gohugo.io/functions/store/)

Returns a Scratch that is not reset on server rebuilds.

The `.Store` method on `.Page` returns a [Scratch](https://gohugo.io/functions/scratch/) to store and manipulate data. In contrast to the `.Scratch` method, this Scratch is not reset on server rebuilds.

### Methods 

#### .Set 

Sets the value of a given key.

```go-html-template
{{ .Store.Set "greeting" "Hello" }}
```

#### .Get 

Gets the value of a given key.

```go-html-template
{{ .Store.Set "greeting" "Hello" }}

{{ .Store.Get "greeting" }} → Hello
```

#### .Add 

Adds a given value to existing value(s) of the given key.

For single values, `Add` accepts values that support Go’s `+` operator. If the first `Add` for a key is an array or slice, the following adds will be appended to that list.

```go-html-template
{{ .Store.Add "greetings" "Hello" }}
{{ .Store.Add "greetings" "Welcome" }}

{{ .Store.Get "greetings" }} → HelloWelcome
{{ .Store.Add "total" 3 }}
{{ .Store.Add "total" 7 }}

{{ .Store.Get "total" }} → 10
{{ .Store.Add "greetings" (slice "Hello") }}
{{ .Store.Add "greetings" (slice "Welcome" "Cheers") }}

{{ .Store.Get "greetings" }} → []interface {}{"Hello", "Welcome", "Cheers"}
```

#### .SetInMap 

Takes a `key`, `mapKey` and `value` and adds a map of `mapKey` and `value` to the given `key`.

```go-html-template
{{ .Store.SetInMap "greetings" "english" "Hello" }}
{{ .Store.SetInMap "greetings" "french" "Bonjour" }}

{{ .Store.Get "greetings" }} → map[french:Bonjour english:Hello]
```

#### .DeleteInMap 

Takes a `key` and `mapKey` and removes the map of `mapKey` from the given `key`.

```go-html-template
{{ .Store.SetInMap "greetings" "english" "Hello" }}
{{ .Store.SetInMap "greetings" "french" "Bonjour" }}
{{ .Store.DeleteInMap "greetings" "english" }}

{{ .Store.Get "greetings" }} → map[french:Bonjour]
```

#### .GetSortedMapValues 

Returns an array of values from `key` sorted by `mapKey`.

```go-html-template
{{ .Store.SetInMap "greetings" "english" "Hello" }}
{{ .Store.SetInMap "greetings" "french" "Bonjour" }}

{{ .Store.GetSortedMapValues "greetings" }} → [Hello Bonjour]
```

#### .Delete 

Removes the given key.

```go-html-template
{{ .Store.Set "greeting" "Hello" }}

{{ .Store.Delete "greeting" }}
```

## 另请参阅

- [.Scratch](https://gohugo.io/functions/scratch/)
- [Menu Variables](https://gohugo.io/variables/menus/)
- [Page Resources](https://gohugo.io/content-management/page-resources/)
