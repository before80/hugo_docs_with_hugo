+++
title = "Cond"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# cond

[https://gohugo.io/functions/cond/](https://gohugo.io/functions/cond/)

Return one of two arguments, depending on the value of a third argument.

## 语法

```
cond CONTROL VAR1 VAR2
```

`cond` returns *VAR1* if *CONTROL* is true, or *VAR2* if it is not.

Example:

```go-html-template
{{ cond (eq (len $geese) 1) "goose" "geese" }}
```

Would emit "goose" if the `$geese` array has exactly 1 item, or "geese" otherwise.

Whenever you use a `cond` function, *both* variable expressions are *always* evaluated. This means that a usage like `cond false (div 1 0) 27` will throw an error because `div 1 0` will be evaluated *even though the condition is false*.

In other words, the `cond` function does *not* provide [short-circuit evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation) and does *not* work like a normal [ternary operator](https://en.wikipedia.org/wiki/%3F:) that will pass over the first expression if the condition returns `false`.
