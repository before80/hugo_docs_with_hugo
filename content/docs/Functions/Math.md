+++
title = "Math"
weight = 67
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# Math

[https://gohugo.io/functions/math/](https://gohugo.io/functions/math/)

Hugo provides mathematical operators in templates.

| Function     | Description                                                  | Example                        |
| :----------- | :----------------------------------------------------------- | :----------------------------- |
| `add`        | Adds two or more numbers.                                    | `{{ add 12 3 2 }}` → `17`      |
|              | *If one of the numbers is a float, the result is a float.*   | `{{ add 1.1 2 }}` → `3.1`      |
| `sub`        | Subtracts one or more numbers from the first number.         | `{{ sub 12 3 2 }}` → `7`       |
|              | *If one of the numbers is a float, the result is a float.*   | `{{ sub 3 2.5 }}` → `0.5`      |
| `mul`        | Multiplies two or more numbers.                              | `{{ mul 12 3 2 }}` → `72`      |
|              | *If one of the numbers is a float, the result is a float.*   | `{{ mul 2 3.1 }}` → `6.2`      |
| `div`        | Divides the first number by one or more numbers.             | `{{ div 12 3 2 }}` → `2`       |
|              | *If one of the numbers is a float, the result is a float.*   | `{{ div 6 4.0 }}` → `1.5`      |
| `mod`        | Modulus of two integers.                                     | `{{ mod 15 3 }}` → `0`         |
| `modBool`    | Boolean of modulus of two integers. Evaluates to `true` if result equals 0. | `{{ modBool 15 3 }}` → `true`  |
| `math.Ceil`  | Returns the least integer value greater than or equal to the given number. | `{{ math.Ceil 2.1 }}` → `3`    |
| `math.Floor` | Returns the greatest integer value less than or equal to the given number. | `{{ math.Floor 1.9 }}` → `1`   |
| `math.Log`   | Returns the natural logarithm of the given number.           | `{{ math.Log 42 }}` → `3.737`  |
| `math.Max`   | Returns the greater of two or more numbers.                  | `{{ math.Max 12 3 2 }}` → `12` |
| `math.Min`   | Returns the smaller of two or more numbers.                  | `{{ math.Min 12 3 2 }}` → `2`  |
| `math.Pow`   | Returns the first number raised to the power of the second number. | `{{ math.Pow 2 3 }}` → `8`     |
| `math.Round` | Returns the nearest integer, rounding half away from zero.   | `{{ math.Round 1.5 }}` → `2`   |
| `math.Sqrt`  | Returns the square root of the given number.                 | `{{ math.Sqrt 81 }}` → `9`     |

## 另请参阅

- [eq](https://gohugo.io/functions/eq/)
- [ge](https://gohugo.io/functions/ge/)
- [gt](https://gohugo.io/functions/gt/)
- [le](https://gohugo.io/functions/le/)
- [lt](https://gohugo.io/functions/lt/)
