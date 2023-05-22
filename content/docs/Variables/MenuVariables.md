+++
title = "菜单变量"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Menu Variables - 菜单变量 

[https://gohugo.io/variables/menus/](https://gohugo.io/variables/menus/)

​	在您的菜单模板中使用这些变量和方法。 

## 变量

​	在[定义菜单项](https://gohugo.io/content-management/menus/#overview)之后，可以在[菜单模板](https://gohugo.io/templates/menu-templates/)中使用以下变量访问其属性。

### .Children

​	(`menu`)当前菜单项下（如果有）的子菜单项的集合。 

### .Identifier

(`string`) 菜单项的 `identifier` 属性。如果您[自动定义菜单项](https://gohugo.io/content-management/menus/#define-automatically)，则为页面的 `.Section`。

### .KeyName

(`string`) 菜单项的 `identifier` 属性，否则为 `name` 属性。

### .Menu

​	(`string`) 包含菜单项的菜单的标识符。

### .Name

​	(`string`) 菜单项的 `name` 属性。

- 如果您[自动定义](https://gohugo.io/content-management/menus/#define-automatically)菜单项，则为页面的 `.LinkTitle`，否则为 `.Title`。

- 如果您在[前置元数据](https://gohugo.io/content-management/menus/#define-in-front-matter)或[站点配置](https://gohugo.io/content-management/menus/#define-in-site-configuration)中定义菜单，则先尝试使用页面的 `.LinkTitle`，然后使用`.Title`。

### .Page

​	(`page`) 与菜单项相关联的页面的引用。

### .Params

​	(`map`) 菜单项的 `params` 属性。

### .Parent

​	(`string`) 菜单项的 `parent` 属性。

### .Post

(`template.HTML`) 菜单项的 `post` 属性。

### .Pre

​	(`template.HTML`) 菜单项的 `pre` 属性。

### .Title

​	(`string`) 菜单项的 `title` 属性。

- 如果您[自动定义](https://gohugo.io/content-management/menus/#define-automatically)菜单项，则为页面的 `.LinkTitle`，否则为 `.Title`。

- 如果您在[前置元数据](https://gohugo.io/content-management/menus/#define-in-front-matter)或[站点配置](https://gohugo.io/content-management/menus/#define-in-site-configuration)中定义菜单，则先尝试使用页面的 `.LinkTitle`，然后使用 `.Title`。

### .URL

​	(`string`) 与菜单项相关联的页面的 `.RelPermalink`。对于指向外部资源的菜单项，使用菜单项的 `url` 属性。

### .Weight

​	(`int`) 菜单项的 `weight` 属性。

- 如果您[自动定义](https://gohugo.io/content-management/menus/#define-automatically)菜单项，则为页面的 `.Weight`。

- 如果您在[前置元数据](https://gohugo.io/content-management/menus/#define-in-front-matter)或[站点配置](https://gohugo.io/content-management/menus/#define-in-site-configuration)中定义菜单，则先尝试使用页面的 `.Weight`。


## 方法 

### .HasChildren

​	(`bool`) 如果 `.Children` 非 nil，则返回 `true`。

### .IsEqual

​	(`bool`) 如果比较的菜单项表示相同的菜单项，则返回 `true`。 

### .IsSameResource

​	(`bool`) 如果比较的菜单条目指向同一资源，则返回`true`。

### .Page.HasMenuCurrent

​	(`bool`) 使用此方法确定活动菜单项的祖先。请参阅[详细信息](https://gohugo.io/functions/hasmenucurrent/)。

### .Page.IsMenuCurrent

​	(`bool`) 使用此方法确定活动菜单项。请参阅[详细信息](https://gohugo.io/functions/ismenucurrent/)。

## 另请参阅 

- [.HasMenuCurrent](https://gohugo.io/functions/hasmenucurrent/)
- [.IsMenuCurrent](https://gohugo.io/functions/ismenucurrent/)
- [.Scratch](https://gohugo.io/functions/scratch/)
- [.Store](https://gohugo.io/functions/store/)
- [文件变量](https://gohugo.io/variables/files/)
