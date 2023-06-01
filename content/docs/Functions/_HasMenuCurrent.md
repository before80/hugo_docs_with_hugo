+++
title = ".HasMenuCurrent"
weight = 5
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

将以下英文翻译为中文：
# .HasMenuCurrent

[https://gohugo.io/functions/hasmenucurrent/](https://gohugo.io/functions/hasmenucurrent/)



## 语法

```
PAGE.HasMenuCurrent MENU MENUENTRY
```

​	`.HasMenuCurrent`  是  `Page`  对象中的一个方法，返回一个布尔值。如果 PAGE 是给定 MENU 中 MENUENTRY 的一个子菜单选项中  `.Page`  的相同对象，则返回true。  

​	如果 MENUENTRY 的`.Page`是一个 [section](https://gohugo.io/content-management/sections/)，则从 Hugo `0.86.0` 开始，此方法对该章节的任何后代也返回true。

​	您可以在 [菜单模板](https://gohugo.io/templates/menu-templates/) 中找到其使用示例。

## 另请参阅

- [.IsMenuCurrent](https://gohugo.io/functions/ismenucurrent/)
- [Menu Templates](https://gohugo.io/templates/menu-templates/)
- [Menu Variables](https://gohugo.io/variables/menus/)
- [Menus](https://gohugo.io/content-management/menus/)
